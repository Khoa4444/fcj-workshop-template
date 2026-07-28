---
title: "Chuẩn bị môi trường"
date: 2026-07-28
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

#### Điều kiện và cấu hình

Cần Python 3.12/tương thích, AWS CLI đã xác thực, S3 bucket và SageMaker execution role. Region mặc định là `ap-southeast-1` nếu không có `AWS_REGION`.

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -c "import boto3, pandas, sklearn, xgboost; print('environment ready')"
aws sts get-caller-identity
aws s3 ls s3://<ten-bucket>
```

Tạo `.env` (không commit): `AWS_REGION`, `S3_BUCKET`, `SAGEMAKER_ROLE_ARN`, `SAGEMAKER_ENDPOINT_NAME`. SageMaker role cần quyền S3 theo prefix và các SageMaker job; Lambda cần `sagemaker:InvokeEndpoint`, CloudWatch Logs và `cloudwatch:PutMetricData`.

{{% notice warning %}}Processing, Training và Endpoint có thể phát sinh chi phí. Kiểm tra account, Region, quota và cleanup trước khi chạy.{{% /notice %}}

> **Ảnh cần bổ sung:** terminal/CloudShell cho `aws sts get-caller-identity` và `aws s3 ls`.
