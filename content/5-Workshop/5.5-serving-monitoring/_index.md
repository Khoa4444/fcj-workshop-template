---
title: "Serving, API, Monitoring, and Testing"
date: 2026-07-28
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

#### Serving and safe operations

```powershell
python scripts/deploy_endpoint.py
python scripts/deploy_endpoint.py --smoke-test
python scripts/deploy_api.py
```

An `ml.m5.large` endpoint serves the selected artifact. Lambda validates JSON and invokes the endpoint; API Gateway exposes `POST /score-agent-run`. Responses include `risk_score`, `quality_score`, `predicted_label`, `decision`, `reasons`, and `probabilities`. Scores below 0.3 allow, 0.3–below 0.7 require review, and scores from 0.7 block; destructive commands always block.

Lambda emits `RiskScore` and `BlockedDecisions` to CloudWatch; Endpoint Data Capture stores all input/output in S3. Default Model Monitor needs flattened payloads or a custom preprocessor before scheduling.

{{% notice warning %}}An `InService` endpoint incurs cost. Historical endpoint, Lambda, and API resources were cleaned up; use historical evidence or redeploy before capturing new screenshots. Never send secrets/tokens/real `.env` content.{{% /notice %}}

> **Image placeholder:** endpoint smoke test, safe/risky API responses, CloudWatch dashboard, and S3 data capture.
