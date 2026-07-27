---
title: "Worklog Tuần 1"
date: 2026-06-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu tuần 1:

* Xác định bài toán rủi ro của AI Coding Agent và phạm vi MVP.
* Làm quen với các dịch vụ AWS/SageMaker cho workflow ML.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Bắt đầu | Hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | Phân tích hành vi đọc tệp, sửa mã, chạy test và tạo summary của coding agent. | 01/06/2026 | 01/06/2026 | `README.md` |
| 3 | Xác định rủi ro: tệp nhạy cảm, lệnh phá hủy, test thiếu bằng chứng và thay đổi ngoài phạm vi. | 02/06/2026 | 02/06/2026 | `data_generation/label_rules.py` |
| 4 | Tìm hiểu S3, Processing, Training, Model Registry, Endpoint, Lambda và API Gateway. | 03/06/2026 | 03/06/2026 | `report/architecture.md` |
| 5 | Thiết kế kiến trúc tổng thể và phạm vi MVP của risk scorer. | 04/06/2026 | 05/06/2026 | Kế hoạch đề tài |
| 6 | Khởi tạo repository và rà soát các module cần triển khai. | 05/06/2026 | 05/06/2026 | Cây thư mục project |

### Kết quả đạt được tuần 1:

* Xác định đánh giá **trajectory** thay vì chỉ output cuối của agent.
* Hoàn thiện MVP gồm simulator/Mini Agent, feature engineering, XGBoost, pipeline và API scoring.
* Nắm kiến trúc MLOps huấn luyện và inference thời gian thực.
* Xác định manual approval và hard safety rule là kiểm soát an toàn bắt buộc.
