---
title: "Pipeline và Model Registry governance"
date: 2026-07-29
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

## Deployment track: đăng ký HPO artifact cho endpoint

Đây là bước **bắt buộc** trước 5.8. `scripts/deploy_endpoint.py` đọc `report/model_registry.json`, nên phải tạo mới file đó bằng HPO artifact của lần chạy hiện tại:

```powershell
python scripts/register_model.py
Get-Content report/model_registry.json
```

Kỳ vọng file có `model_artifact_s3_uri` trỏ tới HPO training job vừa hoàn thành và `approval_status: PendingManualApproval`.

> **[ẢNH PLACEHOLDER — registered HPO model]** SageMaker Console → Model Registry → group `agent-risk-scorer` → package version mới nhất. Ảnh phải thấy `PendingManualApproval`, artifact/metrics liên quan và creation time của run hiện tại. Đây là ảnh model registration, không phải Pipeline graph.

## Pipeline track: orchestration có governance

`pipelines/sagemaker_pipeline.py` định nghĩa Pipeline bằng SageMaker SDK. Đọc code để xác nhận bước và quality gate; command dưới chỉ upsert definition, chưa start execution:

```powershell
python pipelines/sagemaker_pipeline.py
```

## AWS mutation rõ ràng

Command này tạo Processing/Training/Evaluation resources có phí:

```powershell
python pipelines/sagemaker_pipeline.py --execute
```

Theo dõi:

```powershell
aws sagemaker list-pipeline-executions `
  --pipeline-name agent-risk-scorer-pipeline `
  --region ap-southeast-1 `
  --max-results 5
```

Pipeline registration tạo package trong group `agent-risk-scorer` với `ModelApprovalStatus=PendingManualApproval`. Không có step deploy endpoint, dù parameter `DeployEndpoint` có mặt trong definition và default `False`. Pipeline tạo model package governance evidence riêng; endpoint deployment ở 5.8 vẫn dùng `report/model_registry.json` từ deployment track ở trên.

## Governance evidence

`report/pipeline_execution.json` ghi execution ARN kết thúc `djsby9imdlsm` đã `Succeeded`, quality gate `risky_recall >= 0.85`, metrics 1.0 và registered package version 2. `report/model_registry.json` ghi version 1. Cả hai package đều không được auto-approved.

> **[ẢNH PLACEHOLDER — Pipeline execution]** SageMaker Console → Pipelines → `agent-risk-scorer-pipeline` → execution mới nhất. Ảnh phải thấy các step Process, Train, Evaluate, CheckRiskyRecall, RegisterModel đều success và condition `risky_recall >= 0.85` pass. Không dùng ảnh này thay cho ảnh Registry ở phần deployment track.

