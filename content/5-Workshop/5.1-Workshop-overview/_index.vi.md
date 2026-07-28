---
title: "Kiến trúc và mục tiêu"
date: 2026-07-28
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

#### Bài toán và kiến trúc

Patch cuối không đủ để đánh giá độ an toàn của coding agent. Workshop phân tích trajectory gồm thao tác tệp, tool, command, test/lint, diff, safety flags và summary.

```text
Mini Agent → JSON/JSONL → S3 → SageMaker Processing (15 features, 70/15/15)
→ XGBoost Training/HPO → Evaluation (risky_recall >= 0.85) → Model Registry
→ [manual release] Endpoint → Lambda → API Gateway POST /score-agent-run
Endpoint → S3 Data Capture; Lambda → CloudWatch RiskScore/BlockedDecisions
```

> **Ảnh cần bổ sung:** sơ đồ kiến trúc AWS của dự án tại đây.

XGBoost phù hợp feature bảng; `risky_recall` là quality gate; destructive command luôn bị hard-rule `block`; deployment tách khỏi Pipeline và Model Monitor chưa được tạo do input JSON lồng nhau cần flatten/custom preprocessor.
