---
title: "Environment Setup"
date: 2026-07-28
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

#### Requirements and configuration

Use Python 3.12 or compatible, authenticated AWS CLI, an S3 bucket, and a SageMaker execution role. The default region is `ap-southeast-1` unless `AWS_REGION` is set.

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -c "import boto3, pandas, sklearn, xgboost; print('environment ready')"
aws sts get-caller-identity
aws s3 ls s3://<bucket-name>
```

Keep `AWS_REGION`, `S3_BUCKET`, `SAGEMAKER_ROLE_ARN`, and `SAGEMAKER_ENDPOINT_NAME` in an uncommitted `.env` file. SageMaker requires scoped S3/job permissions; Lambda requires endpoint invocation, Logs, and metric permissions.

{{% notice warning %}}Processing, Training, and Endpoint resources may incur charges. Verify account, region, quota, and cleanup first.{{% /notice %}}

> **Image placeholder:** AWS CLI identity and S3-listing evidence.
