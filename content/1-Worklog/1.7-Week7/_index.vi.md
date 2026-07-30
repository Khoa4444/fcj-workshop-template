---
title: "Worklog Tuần 7"
date: 2026-07-13
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Thiết lập observability cho inference và rà soát giới hạn monitoring.
* Kiểm soát chi phí sau demo.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Bắt đầu | Hoàn thành |
| --- | --- | --- | --- |
| 2 | Bật 100% endpoint data capture vào S3. | 13/07/2026 | 13/07/2026 |
| 3 | Ghi `RiskScore` và `BlockedDecisions` từ Lambda vào CloudWatch. | 14/07/2026 | 14/07/2026 |
| 4 | Chuẩn bị dashboard CloudWatch. | 15/07/2026 | 15/07/2026 |
| 5 | Phân tích yêu cầu input phẳng của Default Model Monitor. | 16/07/2026 | 16/07/2026 |
| 6 | Rà soát cleanup endpoint, capture data và tài nguyên còn lại. | 17/07/2026 | 17/07/2026 |

### Kết quả đạt được tuần 7:

* Có S3 data capture 100%, CloudWatch custom metrics và dashboard configuration.
* Ghi nhận Model Monitor schedule chưa tạo vì trajectory JSON lồng nhau cần flattening/custom preprocessor.
* Xác định endpoint phải xóa sau demo để tránh chi phí instance-hour.
