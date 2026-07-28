---
title: "Dọn dẹp tài nguyên"
date: 2026-07-28
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

#### Checklist cleanup

1. Chỉ cleanup sau khi demo/evidence được chấp nhận; không xóa Registry package hoặc Pipeline evidence cần nộp.
2. Xóa SageMaker Endpoint, rồi endpoint configuration không còn dùng.
3. Nếu không dùng API, xóa API Gateway, Lambda và Lambda role theo chính sách IAM.
4. Dừng Model Monitor schedule (nếu được tạo), thiết lập CloudWatch log retention và S3 lifecycle cho data capture/artifact tạm.
5. Kiểm tra không còn Studio/notebook application hoặc Processing/Training job đang chạy.
6. Lưu `report/`, ARN và metric cần cho báo cáo trước khi xóa dữ liệu cloud.

Endpoint demo đã bị xóa để dừng endpoint-hour charges. Trước demo mới, kiểm tra trạng thái cloud hiện tại thay vì dựa vào artifact lịch sử.

> **Ảnh cần bổ sung:** SageMaker Endpoints không còn `agent-risk-scorer-endpoint` hoặc CloudShell xác minh cleanup.
