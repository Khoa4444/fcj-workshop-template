---
title: "Kiến trúc bước 2: Serving và monitoring"
date: 2026-07-29
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---

## Online scoring path

Client POST trajectory JSON tới `POST /score-agent-run`. Lambda parse body, gọi `sagemaker-runtime.invoke_endpoint`, rồi publish `AgentRiskScorer/RiskScore` và `BlockedDecisions`. Endpoint handler chạy `serving/feature_extraction.py`, `predict_proba`, và `serving/decision_policy.py`.

## Monitoring path

`scripts/enable_data_capture.py` tạo endpoint config có 100% JSON Input/Output capture ở `s3://agent-risk-scoring/monitoring/data-capture`. `monitoring/cloudwatch_dashboard.json` mô tả endpoint, Lambda và policy metrics. `monitoring/model_monitor_config.py` ghi rõ cần flattened input trước DefaultModelMonitor.

{{% notice warning %}}
Endpoint, Lambda, API Gateway, dashboard và capture prefix đã bị xóa sau demo. Đây là implementation/configuration giữ trong repo, không phải lời khẳng định chúng đang hoạt động.
{{% /notice %}}

