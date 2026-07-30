---
title: "Worklog Tuần 3"
date: 2026-06-15
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Trích xuất feature từ trajectory và tạo dữ liệu huấn luyện.
* Bảo đảm feature contract giữa preprocessing và inference.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Bắt đầu | Hoàn thành |
| --- | --- | --- | --- |
| 2 | Xác định feature numeric, boolean và source indicator. | 15/06/2026 | 15/06/2026 |
| 3 | Viết `extract_features()` cho JSONL trajectory. | 16/06/2026 | 16/06/2026 |
| 4 | Tạo feature đếm file/tool/command, diff, test/lint và safety flags. | 17/06/2026 | 17/06/2026 |
| 5 | Chia stratified train/validation/test theo 70/15/15. | 18/06/2026 | 18/06/2026 |
| 6 | Đối chiếu feature extractor serving với preprocessing. | 19/06/2026 | 19/06/2026 |

### Kết quả đạt được tuần 3:

* Tạo 15 feature đầu vào và ba tập CSV: 840 train, 180 validation, 180 test.
* Dùng `random_state=42` và stratified split để tái lập kết quả.
* Nhận diện `task_file_relevance_score` và `latency_total_ms` là proxy cần telemetry thực sau này.
