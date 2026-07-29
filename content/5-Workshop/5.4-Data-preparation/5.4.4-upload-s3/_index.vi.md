---
title: "Dataset bước 4: Upload raw JSONL lên S3"
date: 2026-07-29
weight: 4
chapter: false
pre: " <b> 5.4.4. </b> "
---

Lấy bucket do bước 5.2 ghi trong `.env`, xác minh AWS identity, sau đó upload raw input mà notebook/Pipeline dùng:

```powershell
$bucket = ((Get-Content .env | Select-String '^S3_BUCKET=').ToString() -replace '^S3_BUCKET=', '')
aws sts get-caller-identity
aws s3 cp data_generation/sample_trajectories.jsonl `
  "s3://$bucket/raw/sample_trajectories.jsonl" `
  --region ap-southeast-1
aws s3 ls "s3://$bucket/raw/" --region ap-southeast-1
```

Không thay key `raw/sample_trajectories.jsonl`: `notebooks/02_processing.ipynb` và Pipeline đều dùng chính key này. `pipelines/sagemaker_pipeline.py` lấy bucket từ `.env`.

> **[ẢNH PLACEHOLDER — raw input in S3]** S3 Console → bucket vừa tạo ở 5.2 → `raw/` → `sample_trajectories.jsonl`. Chụp object key, size và Last modified. Ảnh này chỉ chứng minh raw dataset đã lên S3.

