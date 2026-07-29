---
title: "Tổng quan workshop"
date: 2026-07-29
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---
## Bài toán và quyết định

Project chấm rủi ro một trajectory AI coding agent, không chấm chất lượng của câu trả lời LLM đơn lẻ. Đầu ra model là probability theo 6 class; policy layer mới quyết định `allow`, `require_review` hoặc `block`.

Người dùng mục tiêu là developer/tooling team đang thử nghiệm coding agent và reviewer cần một tín hiệu trước khi cho agent tiếp tục workflow. API output phục vụ adapter agent, còn Model Registry/Pipeline phục vụ người vận hành ML.

## Mục tiêu và tiêu chí thành công

Một rerun được xem là hoàn thành khi có đủ các bằng chứng sau:

1. JSONL được sinh và nằm ở S3 raw prefix; Processing tạo đủ 3 CSV split.
2. Training/HPO hoàn thành và `report/best_model_metrics.json` có artifact URI/metrics.
3. Pipeline execution `Succeeded`; quality gate dùng `risky_recall >= 0.85`; package Registry ở `PendingManualApproval`.
4. Endpoint trả safe response `allow`, risky response `block`, malformed JSON trả `400`.
5. CloudWatch có `RiskScore`/`BlockedDecisions`; endpoint/API/Lambda được xóa sau demo.

Các tiêu chí trên chứng minh workshop/MLOps flow, không chứng minh model production quality vì data synthetic.

## Phạm vi đã hoàn thiện

Repository có toàn bộ source code cho data generator, preprocessing, training/evaluation, SageMaker Pipeline, serving handler, Lambda, monitoring configuration, deployment/HPO scripts và FastAPI demo. AWS evidence đã ghi nhận tại `report/`; resource online được cleanup sau demo.

## Ranh giới evidence

- Pipeline execution: `Succeeded`, có `risky_recall=1.0`, Register Model package version 2.
- Registry: package version 1 và 2 là `PendingManualApproval`.
- Endpoint/API: historical demo đã từng `InService`/gọi được nhưng hiện **không còn online**.
- Model Monitor schedule: **không có**; input nested trajectory cần flatten trước.

## Cách dùng workshop

Chạy chương 5.2 đến 5.7 trước. Chỉ chạy 5.8 khi sẵn sàng demo request ngay sau đó, và luôn chạy 5.11 ngay khi chụp xong evidence.

## Đóng góp và reflection

Phần tự triển khai của repository gồm trajectory simulator, mock coding agent có tool policy, feature extraction đồng nhất cho training/serving, XGBoost multiclass, policy hard block, SageMaker Pipeline quality gate, Lambda/API adapter và cleanup evidence.

Khó khăn đã ghi nhận là incompatibility XGBoost DataFrame ở Pipeline `EvaluateModel`; source `training/evaluate_pipeline.py` xử lý bằng cách predict với NumPy matrix sau khi cài `xgboost==2.1.4`. Một hạn chế khác là nested inference JSON chưa phù hợp DefaultModelMonitor; project không tạo schedule sai lệch mà ghi rõ cần flatten/custom preprocessor. Hướng phát triển đúng là telemetry thực, human labels, API authentication/throttling, S3 lifecycle/Budgets, endpoint scaling và governed deployment sau manual approval.
