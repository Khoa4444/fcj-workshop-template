---
title: "Chạy SageMaker Processing"
date: 2026-07-29
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

## Local preview miễn phí

Đã chạy ở 5.4.3. Script `preprocessing/processing_script.py` là source chung cho local và Pipeline Processing step.

## Managed Processing qua notebook

Khởi động Jupyter từ repository root rồi mở `notebooks/02_processing.ipynb`:

```powershell
jupyter notebook
```

Chọn kernel `.venv`, sau đó chạy **từng cell từ trên xuống, không bỏ cell**:

1. Cell setup đọc `.env`, đặt `RAW_KEY=raw/sample_trajectories.jsonl` và `PROCESSED_PREFIX=processed`.
2. Cell upload upload JSONL lên S3 (an toàn để chạy lại).
3. Cell `SKLearnProcessor` tạo Processing job `ml.m5.large`, `wait=True`, `logs=True`.
4. Cell verification assert ba object `processed/train.csv`, `processed/validation.csv`, `processed/test.csv`.

Không chạy notebook từ thư mục `notebooks/`: notebook giả định `Path.cwd()` là repository root.

## Managed Processing qua Pipeline

Pipeline cũng tạo Processing job với input:

```text
s3://$bucket/raw/sample_trajectories.jsonl
```

Pipeline lấy `S3_BUCKET` từ `.env` tại runtime. Với account khác không có quyền bucket historical `agent-risk-scoring`, đặt `.env` sang bucket thuộc account của bạn nhưng giữ nguyên raw key `raw/sample_trajectories.jsonl`. Chạy Pipeline ở 5.7 để thực hiện full sequence.

Output managed Processing là `train.csv`, `validation.csv`, `test.csv` ở Processing output S3 URI, rồi được nối vào Training channels.

> **[ẢNH PLACEHOLDER — SageMaker Processing job]** SageMaker Console → Processing jobs → job vừa tạo → Overview. Ảnh phải chỉ thấy job name, `Completed`, instance `ml.m5.large`, input `raw/sample_trajectories.jsonl` và output prefix `processed/`. Không đưa HPO/Registry vào ảnh này.

> **[ẢNH PLACEHOLDER — processed CSV objects]** S3 Console → bucket của bạn → `processed/`. Ảnh phải thấy đúng ba object `train.csv`, `validation.csv`, `test.csv`. Đây là ảnh chứng minh output Processing, không phải raw JSONL.

