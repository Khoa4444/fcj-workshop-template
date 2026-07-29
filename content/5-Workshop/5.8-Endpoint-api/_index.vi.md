---
title: "Endpoint và scoring API"
date: 2026-07-29
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

{{% notice warning %}}
Các command trong chương này tạo endpoint `ml.m5.large`, Lambda và HTTP API có phí. Endpoint historical đã bị xóa. Chạy phần này chỉ khi bạn có đủ thời gian chụp evidence và cleanup ngay tại 5.11.
{{% /notice %}}

## Deploy endpoint

`scripts/deploy_endpoint.py` đọc `report/model_registry.json`, tạo `SKLearnModel` với `serving/inference.py` và deploy model artifact.

```powershell
Get-Content report/model_registry.json
python scripts/deploy_endpoint.py

aws sagemaker describe-endpoint `
  --endpoint-name agent-risk-scorer-endpoint `
  --region ap-southeast-1 `
  --query "EndpointStatus" `
  --output text

python scripts/deploy_endpoint.py --smoke-test
```

Chỉ tiếp tục khi status là `InService`. Historical evidence trong `report/endpoint_deployment.json` ghi endpoint status `InService`, nhưng cleanup report xác nhận nó đã bị xóa sau đó.

> **[ẢNH PLACEHOLDER — SageMaker endpoint InService]** SageMaker Console → Inference → Endpoints → `agent-risk-scorer-endpoint`. Ảnh phải thấy Endpoint status `InService`, endpoint name và instance type `ml.m5.large`. Không hiển thị API response hoặc Registry ở ảnh này.

## Deploy Lambda và API Gateway

```powershell
if (Test-Path report/api_gateway.json) {
  Copy-Item report/api_gateway.json report/api_gateway.historical.json
  Remove-Item report/api_gateway.json
}
python scripts/deploy_api.py
$api = (Get-Content report/api_gateway.json | ConvertFrom-Json).score_api_url
$api
```

`report/api_gateway.json` trong repository là historical evidence của API đã cleanup. Khối backup/remove ở trên là bắt buộc cho rerun hiện tại: source `scripts/deploy_api.py` sẽ tái sử dụng file nếu nó còn tồn tại. Script sau đó tạo Lambda `agent-risk-scorer-api`, role `agent-risk-scorer-lambda-role`, HTTP API `agent-risk-scorer-api`, route `POST /score-agent-run`, CORS cho `POST`/`OPTIONS`, và quyền `sagemaker:InvokeEndpoint` cho endpoint name cấu hình.

> **[ẢNH PLACEHOLDER — API Gateway route]** API Gateway Console → APIs → API vừa tạo → Routes. Ảnh phải chỉ thấy `POST /score-agent-run` và Lambda integration. Đây là evidence API layer, không phải ảnh endpoint.

## Safe request

```powershell
$safe = @{
  source = "mini_llm_agent"; tools_called = @("read_file", "run_tests")
  files_read = @("demo_repo/app/auth.py"); files_modified = @("demo_repo/app/auth.py")
  commands_run = @("pytest demo_repo/tests"); tests_passed = $true; lint_passed = $true
  diff_lines_added = 4; diff_lines_deleted = 1; touched_sensitive_files = $false
  destructive_command_detected = $false; used_network_command = $false; summary_claim_supported = $true
} | ConvertTo-Json -Depth 4
Invoke-RestMethod -Uri $api -Method Post -ContentType "application/json" -Body $safe
```

## Risky request

```powershell
$risky = @{
  source = "simulator"; tools_called = @("read_file", "edit_file", "run_tests")
  files_read = @("demo_repo/app/auth.py"); files_modified = @(".env")
  commands_run = @("rm -rf /tmp/data"); tests_passed = $false; lint_passed = $false
  diff_lines_added = 250; diff_lines_deleted = 120; touched_sensitive_files = $true
  destructive_command_detected = $true; used_network_command = $false; summary_claim_supported = $false
} | ConvertTo-Json -Depth 4
Invoke-RestMethod -Uri $api -Method Post -ContentType "application/json" -Body $risky
```

Kỳ vọng risky response có `decision: block` và reason `Destructive command detected`, vì hard rule override score model.

> **[ẢNH PLACEHOLDER — safe scoring response]** Chụp terminal chỉ với safe request response. Cần thấy `risk_score`, `predicted_label`, `decision: allow` và `reasons`; che API URL nếu ảnh public.

> **[ẢNH PLACEHOLDER — risky policy block]** Chụp terminal chỉ với risky request response. Cần thấy `decision: block` và `Destructive command detected`; đây là evidence hard safety rule.

