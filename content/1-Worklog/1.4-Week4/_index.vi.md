---
title: "Worklog Tuần 4"
date: 2026-06-22
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Huấn luyện và đánh giá model phân loại rủi ro.
* Xác định metric an toàn làm quality gate.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Bắt đầu | Hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | Xây training script XGBoost đa lớp và LabelEncoder. | 22/06/2026 | 22/06/2026 | `train_xgboost.py` |
| 3 | Lưu model và encoder thành artifact inference. | 23/06/2026 | 23/06/2026 | `xgboost_model.json` |
| 4 | Viết evaluator cho held-out test set. | 24/06/2026 | 24/06/2026 | `evaluate_pipeline.py` |
| 5 | Đánh giá accuracy, macro F1, risky recall và false-negative rate. | 25/06/2026 | 25/06/2026 | `evaluation_report.json` |
| 6 | Chọn `risky_recall >= 0.85` làm quality gate. | 26/06/2026 | 26/06/2026 | `sagemaker_pipeline.py` |

### Kết quả đạt được tuần 4:

* Có XGBoost multiclass classifier với `multi:softprob` và evaluation trên 180 sample simulator.
* Ghi nhận accuracy 1.0, macro F1 1.0, risky recall 1.0, false-negative rate 0.0.
* Các metric hoàn hảo chỉ xác nhận workflow trên dữ liệu synthetic, không phải hiệu năng production.
