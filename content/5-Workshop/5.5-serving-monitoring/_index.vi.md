---
title: "Serving, API, monitoring và kiểm thử"
date: 2026-07-28
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

#### Serving và vận hành an toàn

```powershell
python scripts/deploy_endpoint.py
python scripts/deploy_endpoint.py --smoke-test
python scripts/deploy_api.py
```

Endpoint `ml.m5.large` dùng artifact được chọn, Lambda validate JSON rồi gọi `InvokeEndpoint`, API Gateway cung cấp `POST /score-agent-run`. Response trả `risk_score`, `quality_score`, `predicted_label`, `decision`, `reasons`, `probabilities`. Policy: score dưới 0.3 là `allow`, 0.3–dưới 0.7 là `require_review`, từ 0.7 là `block`; destructive command luôn `block`.

Lambda ghi `RiskScore`, `BlockedDecisions` vào CloudWatch; Endpoint Data Capture ghi 100% input/output vào S3. Default Model Monitor chưa có schedule do raw trajectory JSON lồng nhau, cần flattened payload/custom preprocessor.

{{% notice warning %}}Endpoint tính phí khi `InService`. Endpoint, Lambda và API historical đã cleanup; chỉ dùng evidence lịch sử hoặc redeploy để chụp lại. Không gửi secret/token/.env thật vào API hoặc data capture.{{% /notice %}}

> **Ảnh cần bổ sung:** endpoint InService/smoke test, API safe+risky response, CloudWatch metrics/dashboard và S3 data capture.
