---
title: "Bản đề xuất"
date: 2026-07-28
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# AI Coding Agent Risk Scorer trên AWS SageMaker

## 1. Tổng quan dự án

AI Coding Agent Risk Scorer đánh giá rủi ro của từng lần thực thi AI Coding Agent. Thay vì chỉ xem patch hoặc câu trả lời cuối, hệ thống lưu **trajectory log** gồm thao tác tệp, công cụ, lệnh, kết quả test/lint, kích thước diff, dấu hiệu tệp nhạy cảm và summary của agent.

Trajectory được chuyển thành feature dạng bảng. Model XGBoost dự đoán nhãn vận hành, `risk_score` và `quality_score`; decision policy kết hợp kết quả model với hard safety rules để trả `allow`, `require_review` hoặc `block`.

Project sử dụng Amazon S3, SageMaker Processing, Training, HPO, Model Registry, Pipelines, Endpoint, AWS Lambda, API Gateway, CloudWatch và S3 Data Capture. Pipeline đã chạy thành công và đăng ký model package version 2 với trạng thái `PendingManualApproval`.

## 2. Mục tiêu

1. Chuẩn hóa trajectory log cho các lần chạy coding agent.
2. Sinh dữ liệu mô phỏng có nhãn, trích xuất feature bằng SageMaker Processing.
3. Huấn luyện XGBoost đa lớp, đánh giá held-out test split và tối ưu hyperparameter.
4. Dùng `risky_recall` làm quality gate trước khi đăng ký Model Registry.
5. Cung cấp API `POST /score-agent-run` trả risk decision cho trajectory.
6. Chặn destructive command và kiểm duyệt hành vi nhạy cảm bằng rule-based guardrails.
7. Ghi inference data capture vào S3, custom metrics vào CloudWatch.
8. Duy trì manual approval, tách registration/training khỏi release endpoint.

## 3. Vấn đề cần giải quyết

Output cuối của AI Coding Agent không phản ánh liệu quá trình thực thi có an toàn hay không. Rủi ro gồm sửa tệp ngoài phạm vi; chạm `.env`, secret, credential, CI/CD hoặc cấu hình deployment; chạy lệnh phá hủy; báo test pass khi không có bằng chứng; và tạo diff lớn cần reviewer kiểm tra.

Hệ thống phân loại trajectory thành `safe`, `require_review`, `wrong_tool`, `hallucinated_success`, `risky` và `failed`. Model ước lượng xác suất rủi ro, còn policy bảo đảm hành vi nguy hiểm rõ ràng được xử lý bằng guardrail thay vì chỉ dựa vào ML.

## 4. Kiến trúc giải pháp

Luồng xử lý: **Mini Coding Agent/Agent Runner → Trajectory JSON/JSONL → Amazon S3 → SageMaker Processing (15 feature, train/validation/test 70/15/15) → SageMaker Training/HPO → Model Registry → Endpoint → Lambda → API Gateway → Client/Demo CLI**.

SageMaker Pipelines tự động hóa: **Processing → Training → Evaluation → CheckRiskyRecall → RegisterModel**. Endpoint deployment là release step riêng, không tự động chạy trong Pipeline. Monitoring gồm Endpoint → S3 Data Capture và Lambda → CloudWatch custom metrics/dashboard.

> **Vị trí ảnh 1 — Sơ đồ kiến trúc tổng thể:** sẽ chèn ảnh tại đây. Đường dẫn dự kiến: `/images/2-Proposal/architecture-overview.png`.

> **Vị trí ảnh 2 — Luồng MLOps và inference:** sẽ chèn ảnh tại đây. Đường dẫn dự kiến: `/images/2-Proposal/mlops-inference-flow.png`.

| Thành phần | Vai trò |
| --- | --- |
| Mini Agent | Tạo trajectory từ thao tác đọc/sửa tệp và chạy test |
| S3 | Lưu raw trajectory, processed CSV, model artifact, report và data capture |
| SageMaker Processing | Trích xuất 15 feature và chia dữ liệu 70/15/15 |
| SageMaker Training/HPO | Huấn luyện/tối ưu XGBoost theo `validation:macro_f1` |
| Pipeline/Registry | Kiểm tra `risky_recall >= 0.85`, đăng ký model chờ duyệt |
| Endpoint/Lambda/API Gateway | Cung cấp inference qua `POST /score-agent-run` |
| CloudWatch/S3 Data Capture | Ghi `RiskScore`, `BlockedDecisions` và inference evidence |

## 5. Timeline

| Tuần | Công việc chính | Deliverable | Trạng thái |
| --- | --- | --- | --- |
| 1 | Phân tích rủi ro, xác định MVP và kiến trúc | Architecture, repo skeleton | Hoàn thành |
| 2 | Generator, schema và label rules | JSONL 1.200 record | Hoàn thành |
| 3 | Feature engineering và data split | CSV train/validation/test | Hoàn thành |
| 4 | XGBoost và held-out evaluation | Model artifact, metrics | Hoàn thành |
| 5 | HPO, Registry và Pipeline | HPO metadata, model package | Hoàn thành |
| 6 | Endpoint, Lambda/API Gateway, API demo | Serving/API evidence | Cần redeploy để demo lại |
| 7 | Data capture và CloudWatch | Monitoring configuration | Hoàn thành một phần |
| 8 | Báo cáo, worklog và roadmap | Documentation/evidence | Hoàn thành |

## 6. Rủi ro và giảm thiểu

| Rủi ro | Ảnh hưởng | Biện pháp giảm thiểu |
| --- | --- | --- |
| Dữ liệu synthetic không đại diện agent thật | Cao | Thu thập trajectory thực, human labeling; không diễn giải metric là production |
| Bỏ sót run `risky` | Cao | Quality gate risky recall, theo dõi false-negative rate |
| Thao tác nguy hiểm | Cao | Tool policy và hard `block` rule |
| Training-serving feature lệch nhau | Trung bình | Shared feature package, contract/regression tests |
| Model Monitor không nhận JSON lồng nhau | Trung bình | Flatten payload hoặc custom preprocessor |
| Endpoint gây chi phí liên tục | Trung bình | Chỉ deploy khi demo và cleanup sau đó |
| IAM/API chưa production-grade | Cao | IAM policy audit, authentication và rate limiting |

## 7. Tài liệu tham chiếu nội bộ

`README.md`, `report/architecture.md`, `report/pipeline_execution.json`, `report/best_model_metrics.json`, `report/model_registry.json`, `report/endpoint_deployment.json`, `report/api_gateway.json`, `report/monitoring_setup.json`.
