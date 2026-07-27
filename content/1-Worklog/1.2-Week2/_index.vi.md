---
title: "Worklog Tuần 2"
date: 2026-06-08
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

* Xây dựng dữ liệu trajectory mô phỏng và quy tắc gán nhãn.
* Chuẩn hóa schema cho các lần chạy agent.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Bắt đầu | Hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | Thiết kế sáu nhãn: `safe`, `require_review`, `wrong_tool`, `hallucinated_success`, `risky`, `failed`. | 08/06/2026 | 08/06/2026 | `label_rules.py` |
| 3 | Định nghĩa task, files, commands, test/lint, diff, safety flags và summary. | 09/06/2026 | 09/06/2026 | `sample_trajectories.jsonl` |
| 4 | Viết generator cho scenario an toàn, risky, review, wrong-tool và failed. | 10/06/2026 | 10/06/2026 | `generate_scenarios.py` |
| 5 | Sinh 1.200 JSONL record với seed 42 và kiểm tra nhãn. | 11/06/2026 | 11/06/2026 | `sample_trajectories.jsonl` |
| 6 | Rà soát giới hạn dữ liệu synthetic để ghi nhận trong báo cáo. | 12/06/2026 | 12/06/2026 | `final_report_vi.md` |

### Kết quả đạt được tuần 2:

* Có dataset mô phỏng 1.200 trajectory tái lập được bằng seed 42.
* Có rule phát hiện tệp nhạy cảm, destructive command và summary không có bằng chứng.
* Phân biệt dữ liệu simulator với dữ liệu agent thực; không diễn giải metric synthetic là production.
* Chuẩn bị JSONL cho SageMaker Processing.
