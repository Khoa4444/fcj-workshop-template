---
title: "Kiểm tra end-to-end và evidence"
date: 2026-07-29
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

## Free local validation

Chạy test app và mock agent:

```powershell
pytest demo_repo/tests -q
python -m agent.agent_runner `
  --task "Fix login validation bug" `
  --output runs/run_login.json
Get-Content runs/run_login.json
```

Agent mock lần lượt đọc `demo_repo/app/auth.py`, thử sửa token validation, chạy `pytest demo_repo/tests`, và ghi JSON trajectory. Nếu source đã được sửa trong run cũ, `old_text` có thể không còn; dùng working tree sạch hoặc restore dòng `return token == "valid-token"` trước khi muốn lặp lại hành vi edit thành công.

## Live API integration

Sau 5.8, dùng URL `$api` mới:

```powershell
python -m agent.agent_runner `
  --task "Fix login validation bug" `
  --output runs/run_login_api.json `
  --score-api-url $api
```

Agent in `Risk Score`, `Quality Score`, `Decision`, `Reasons`; trajectory được lưu cục bộ. Historical evidence `report/agent_api_demo.json` ghi một run end-to-end `require_review` với risk score `0.3152`; không dùng đó để thay response live mới.

## Negative request và Lambda logs

Lambda handler trả HTTP `400` nếu request body không phải JSON. Kiểm tra đúng error contract bằng lệnh sau:

```powershell
try {
  Invoke-WebRequest -Uri $api -Method Post -ContentType "application/json" -Body '{not-json'
} catch {
  $response = $_.Exception.Response
  "HTTP $([int]$response.StatusCode)"
  $reader = New-Object System.IO.StreamReader($response.GetResponseStream())
  $reader.ReadToEnd()
}
```

Kỳ vọng: `HTTP 400` và body có `Request body must be valid JSON.`. Đây là test malformed input; safe/risky test ở 5.8 là test business/policy behavior.

Sau một request, xem Lambda log group của lần deploy hiện tại:

```powershell
aws logs tail /aws/lambda/agent-risk-scorer-api `
  --since 10m `
  --follow `
  --region ap-southeast-1
```

Dừng tail bằng `Ctrl+C`. Lambda source không tự ghi structured application log; output ở đây chủ yếu là invocation/platform/error logs của Lambda. Không diễn giải absence of error log là metric model quality.

## Evidence checklist

- terminal generate JSONL và 1200 lines;
- Processing completed + ba CSV output;
- Training/HPO completed + best metrics report;
- Pipeline succeeded + Registry PendingManualApproval;
- endpoint InService;
- safe API response và risky block response;
- CloudWatch datapoint sau API call;
- cleanup confirmation.

> **[ẢNH PLACEHOLDER — end-to-end agent]** Chụp terminal agent có phần `AGENT RISK SCORING EVALUATION` và file `runs/run_login_api.json` trong Explorer. Không hiển thị API URL nếu không được phép.

> **[ẢNH PLACEHOLDER — malformed-request validation]** Chụp terminal chỉ với `HTTP 400` và JSON message `Request body must be valid JSON.`. Ảnh này chứng minh API input validation, không dùng thay ảnh safe/risky decision.

> **[ẢNH PLACEHOLDER — Lambda logs]** CloudWatch Console → Log groups → `/aws/lambda/agent-risk-scorer-api` → log stream mới nhất. Ảnh phải có timestamp ngay sau request test; chỉ dùng để chứng minh observability của Lambda.

