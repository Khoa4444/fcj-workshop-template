---
title: "Cleanup"
date: 2026-07-29
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---

{{% notice warning %}}
Chỉ chạy lệnh xóa này cho resource bạn vừa tạo trong demo và đã xác minh name/region. Endpoint phải được xóa đầu tiên để dừng endpoint-hour charges.
{{% /notice %}}

## 1. Xóa endpoint và endpoint configuration

Lưu config name trước khi delete endpoint nếu chưa lưu ở bước deploy:

```powershell
$region = "ap-southeast-1"
$endpoint = "agent-risk-scorer-endpoint"
$endpointConfig = aws sagemaker describe-endpoint `
  --endpoint-name $endpoint `
  --region $region `
  --query "EndpointConfigName" `
  --output text

aws sagemaker delete-endpoint --endpoint-name $endpoint --region $region
aws sagemaker wait endpoint-deleted --endpoint-name $endpoint --region $region
aws sagemaker delete-endpoint-config --endpoint-config-name $endpointConfig --region $region
```

## 2. Xóa API Gateway và Lambda

`report/api_gateway.json` được deploy script ghi đè bằng API mới. Lấy ID từ file rồi xóa đúng API đó:

```powershell
$apiId = (Get-Content report/api_gateway.json | ConvertFrom-Json).api_id
aws apigatewayv2 delete-api --api-id $apiId --region $region
aws lambda delete-function --function-name agent-risk-scorer-api --region $region
```

Lambda IAM role `agent-risk-scorer-lambda-role` chỉ xóa khi chắc chắn không được resource nào khác sử dụng. Script có inline policy `invoke-agent-risk-scorer`; kiểm tra trước khi xóa role.

## 3. Xóa dashboard, optional alarm và monitoring demo data

Nếu đã tạo dashboard/optional alarm ở 5.10, xóa chúng:

```powershell
aws cloudwatch delete-dashboards --dashboard-names agent-risk-scorer-dashboard --region $region
aws cloudwatch delete-alarms --alarm-names agent-risk-scorer-blocked-decisions-demo --region $region
```

`delete-alarms` an toàn nếu alarm name không tồn tại; chỉ áp dụng cho alarm demo ở 5.10, không xóa alarm của workload khác.

Xem trước prefix trước mọi thao tác:

```powershell
aws s3 ls s3://agent-risk-scoring/monitoring/data-capture/ --recursive --region $region
```

Chỉ khi không còn cần evidence capture, xóa đúng prefix đó:

```powershell
aws s3 rm s3://agent-risk-scoring/monitoring/data-capture/ --recursive --region $region
```

Không xóa raw data, processed/model artifacts, Pipeline execution hay Registry package nếu còn cần evidence/reproducibility.

## 4. Tùy chọn: xóa workshop bucket và execution role

Chỉ làm bước này sau khi đã tải/copy toàn bộ evidence cần nộp. Lệnh xóa toàn bộ object trong bucket workshop do bước 5.2 tạo:

```powershell
$bucket = ((Get-Content .env | Select-String '^S3_BUCKET=').ToString() -replace '^S3_BUCKET=', '')
aws s3 rb "s3://$bucket" --force --region $region

$roleName = "agent-risk-scorer-sagemaker-execution-role"
aws iam delete-role-policy --role-name $roleName --policy-name agent-risk-scorer-s3-access
aws iam detach-role-policy --role-name $roleName --policy-arn arn:aws:iam::aws:policy/AmazonSageMakerFullAccess
aws iam delete-role --role-name $roleName
Remove-Item sagemaker-trust-policy.json, sagemaker-s3-policy.json -ErrorAction SilentlyContinue
```

Không chạy lệnh này với bucket/role shared hoặc historical evidence của người khác. Trong trường hợp chỉ cần dừng chi phí lớn, endpoint/API/Lambda cleanup ở bước 1–2 là ưu tiên trước.

## Final absence checklist

```powershell
aws sagemaker list-endpoints --region $region `
  --query "Endpoints[?EndpointName=='agent-risk-scorer-endpoint'].EndpointStatus"
aws lambda get-function --function-name agent-risk-scorer-api --region $region
```

Lệnh Lambda cuối kỳ vọng lỗi `ResourceNotFoundException`; đó là xác nhận delete thành công. Với API, Console không còn API ID vừa xóa.

## Historical cleanup evidence

`report/cleanup_report.json` ghi cleanup ngày 2026-07-26: endpoint, endpoint configurations, HTTP API, Lambda, Lambda role, dashboard, log groups và data-capture prefix đã bị xóa; Pipeline, Model Registry versions, S3 artifacts và Studio Domain không có app chạy được giữ lại.

> **[ẢNH PLACEHOLDER — cleanup]** Chụp terminal `list-endpoints` trả mảng rỗng cho endpoint name, và SageMaker Endpoints Console không có endpoint đó. Chụp trước khi đóng cửa sổ demo; đây là evidence kiểm soát chi phí quan trọng.

