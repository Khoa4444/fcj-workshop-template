---
title: "Worklog Tuần 5"
date: 2026-06-29
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Tối ưu model và quản trị version trong Model Registry.
* Tạo pipeline tự động chỉ đăng ký model đạt điều kiện.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Bắt đầu | Hoàn thành |
| --- | --- | --- | --- |
| 2 | Cấu hình HPO với objective `validation:macro_f1`. | 29/06/2026 | 29/06/2026 |
| 3 | Rà soát best job và hyperparameter đã chọn. | 30/06/2026 | 30/06/2026 |
| 4 | Tạo model package group `agent-risk-scorer`. | 01/07/2026 | 01/07/2026 |
| 5 | Thiết kế Pipeline gồm Processing, Training, Evaluation và ConditionStep. | 02/07/2026 | 02/07/2026 |
| 6 | Đặt approval status mặc định là `PendingManualApproval`. | 03/07/2026 | 03/07/2026 |

### Kết quả đạt được tuần 5:

* Có HPO metadata với `max_depth=4` và `n_estimators=207`.
* Có Model Registry package group và cơ chế phê duyệt thủ công.
* Pipeline chỉ `RegisterModel` khi risky recall đạt 0.85; registration tách khỏi deployment.
