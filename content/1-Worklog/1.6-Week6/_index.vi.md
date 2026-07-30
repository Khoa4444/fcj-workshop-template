---
title: "Worklog Tuần 6"
date: 2026-07-06
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Xây dựng decision policy và luồng inference thời gian thực.
* Kết nối endpoint với Lambda và API Gateway.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Bắt đầu | Hoàn thành |
| --- | --- | --- | --- |
| 2 | Viết inference handler nhận JSON trajectory và trả xác suất lớp. | 06/07/2026 | 06/07/2026 |
| 3 | Xây decision policy với score threshold và hard safety rule. | 07/07/2026 | 07/07/2026 |
| 4 | Viết Lambda gọi `InvokeEndpoint`, validate JSON và trả CORS response. | 08/07/2026 | 08/07/2026 |
| 5 | Cấu hình `POST /score-agent-run` và smoke test endpoint. | 09/07/2026 | 09/07/2026 |
| 6 | Chạy Mini Agent demo, lưu trajectory và API response. | 10/07/2026 | 10/07/2026 |

### Kết quả đạt được tuần 6:

* Endpoint trả `risk_score`, `quality_score`, nhãn, decision, reasons và class probabilities.
* Lệnh destructive bị `block`; thay đổi tệp nhạy cảm yêu cầu review hoặc block theo score.
* Có evidence API end-to-end với decision `require_review`.
* Endpoint là tài nguyên ngắn hạn và cần redeploy sau cleanup nếu trình diễn lại.
