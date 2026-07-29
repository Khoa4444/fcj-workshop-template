---
title: "Kiến trúc và data flow"
date: 2026-07-29
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

Chương này tách architecture thành hai nhánh: data-to-registry và online scoring. Không có VPC endpoint, multi-region deployment hay Model Monitor schedule trong source hiện tại.

## Thành phần theo trách nhiệm

| Thành phần | Source | Trách nhiệm |
| --- | --- | --- |
| Agent/simulator | `agent/`, `data_generation/` | tạo raw trajectory |
| Preprocess | `preprocessing/processing_script.py` | feature + 70/15/15 split |
| ML | `training/` | train, evaluation, HPO metrics |
| Orchestrator | `pipelines/sagemaker_pipeline.py` | processing/train/evaluate/gate/register |
| Serving | `serving/` | feature extraction, probability, policy |
| API | `lambda/lambda_handler.py` | invoke endpoint, metrics, CORS |
| Observability | `monitoring/` | dashboard definition + capture config |

## Lý do chọn AWS services

| Service | Lý do phù hợp với project |
| --- | --- |
| Amazon S3 | Object storage phù hợp JSONL/CSV/model artifact/report; input/output giữa SageMaker jobs dùng S3 URI. |
| SageMaker Processing | Chạy feature engineering và split trong managed job, không cần quản trị processing server. |
| SageMaker Training/HPO/Pipelines | Tách training jobs, metric tracking, conditional quality gate và model registration thành lifecycle có thể kiểm tra lại. |
| Model Registry | Giữ version model và `PendingManualApproval`, tách metric pass khỏi release decision. |
| SageMaker Endpoint | Cung cấp synchronous real-time inference để Lambda gọi trong demo. |
| Lambda + API Gateway | Serverless request path cho một HTTP route, không cần duy trì web server riêng. |
| CloudWatch + Data Capture | Lưu service/custom metrics và request/response inference phục vụ demo/observability. |

Project không dùng DynamoDB, SQS, VPC endpoint hay Application Auto Scaling. Không thêm chúng vào architecture diagram hoặc nói chúng đã triển khai. Lambda có tính event-driven theo request HTTP; endpoint hiện dùng một instance `ml.m5.large`, chưa có autoscaling policy.

> **[ẢNH PLACEHOLDER — architecture]** Render Mermaid trong `README.md` hoặc `report/architecture.md`. Chú thích ảnh phải nêu endpoint/API là historical resources đã cleanup.

