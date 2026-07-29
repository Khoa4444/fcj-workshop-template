---
title: "Chuẩn bị và safety gate"
date: 2026-07-29
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

## Yêu cầu local

Mở PowerShell tại repository root. Các lệnh dưới đây cài mọi dependency cần cho source code và mở notebook khi cần chạy managed Processing/Training:

```powershell
cd "C:\Users\Lenovo\Desktop\kortav\ai-coding-agent-risk-scorer"
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
pip install notebook
python -c "import pandas, xgboost, sagemaker; print('Environment ready')"
pytest demo_repo/tests -q
```

Kỳ vọng: `3 passed`. Nếu khác, dừng ở đây và sửa local environment trước khi tạo AWS resource.

## AWS configuration: tạo resource cho account đang chạy

Không dùng bucket/role historical của report nếu account của bạn không sở hữu chúng. Khối lệnh này tự lấy AWS account hiện tại, tạo bucket có tên duy nhất, chặn public access, tạo SageMaker execution role, rồi ghi `.env` mà toàn bộ script/notebook trong project đọc.

AWS identity hiện tại cần được cấp quyền tạo S3 bucket/IAM role/policy. Nếu `AccessDenied`, administrator phải cấp quyền đó; không thay ARN bằng giá trị đoán mò.

```powershell
$region = "ap-southeast-1"
$accountId = aws sts get-caller-identity --query "Account" --output text
$bucket = "agent-risk-scoring-$accountId-$(Get-Random -Minimum 1000 -Maximum 9999)"
$roleName = "agent-risk-scorer-sagemaker-execution-role"

aws s3 mb "s3://$bucket" --region $region
aws s3api put-public-access-block --bucket $bucket --public-access-block-configuration "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true"
aws s3api put-bucket-encryption --bucket $bucket --server-side-encryption-configuration '{"Rules":[{"ApplyServerSideEncryptionByDefault":{"SSEAlgorithm":"AES256"}}]}'

@'
{"Version":"2012-10-17","Statement":[{"Effect":"Allow","Principal":{"Service":"sagemaker.amazonaws.com"},"Action":"sts:AssumeRole"}]}
'@ | Set-Content -Encoding utf8 sagemaker-trust-policy.json

aws iam create-role --role-name $roleName --assume-role-policy-document file://sagemaker-trust-policy.json
aws iam attach-role-policy --role-name $roleName --policy-arn arn:aws:iam::aws:policy/AmazonSageMakerFullAccess

@"
{"Version":"2012-10-17","Statement":[{"Effect":"Allow","Action":["s3:GetObject","s3:PutObject","s3:DeleteObject","s3:ListBucket"],"Resource":["arn:aws:s3:::$bucket","arn:aws:s3:::$bucket/*"]}]}
"@ | Set-Content -Encoding utf8 sagemaker-s3-policy.json

aws iam put-role-policy --role-name $roleName --policy-name agent-risk-scorer-s3-access --policy-document file://sagemaker-s3-policy.json
$roleArn = aws iam get-role --role-name $roleName --query "Role.Arn" --output text

@"
AWS_REGION=$region
S3_BUCKET=$bucket
SAGEMAKER_ROLE_ARN=$roleArn
SAGEMAKER_ENDPOINT_NAME=agent-risk-scorer-endpoint
LLM_PROVIDER=mock
"@ | Set-Content -Encoding utf8 .env
Get-Content .env
```

{{% notice warning %}}
`AmazonSageMakerFullAccess` được dùng để workshop có thể chạy đơn giản. Đây không phải least-privilege production policy. Project tách SageMaker execution role và Lambda role; trước production cần giới hạn actions/resources theo job, bucket và endpoint thực tế.
{{% /notice %}}

## Confirmation gate cho paid resources

Processing, Training/HPO, endpoint `ml.m5.large`, Lambda và HTTP API có thể phát sinh chi phí. Trước bước 5.5, ghi lại account, region, endpoint name, người cleanup và deadline cleanup. Không sử dụng URL historical trong `report/api_gateway.json` vì API đó đã xóa.

> **[ẢNH PLACEHOLDER — environment ready]** Chụp duy nhất terminal có `Environment ready`, `3 passed`, `aws sts get-caller-identity`, và `.env` nhưng che `SAGEMAKER_ROLE_ARN`. Ảnh này chỉ chứng minh prerequisite, không dùng để minh họa Processing/Training.

