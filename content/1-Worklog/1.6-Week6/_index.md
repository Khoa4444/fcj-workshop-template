---
title: "Week 6 Worklog"
date: 2026-07-06
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Build the decision policy and real-time inference flow.
* Connect the endpoint to Lambda and API Gateway.

### Tasks carried out this week:

| Day | Task | Start | Completion |
| --- | --- | --- | --- |
| Mon | Implemented an inference handler that accepts trajectory JSON and returns class probabilities. | 06/07/2026 | 06/07/2026 |
| Tue | Built a decision policy with score thresholds and hard safety rules. | 07/07/2026 | 07/07/2026 |
| Wed | Implemented Lambda endpoint invocation, JSON validation, and CORS responses. | 08/07/2026 | 08/07/2026 |
| Thu | Configured `POST /score-agent-run` and smoke-tested the endpoint. | 09/07/2026 | 09/07/2026 |
| Fri | Ran the Mini Agent demo and captured trajectory and API responses. | 10/07/2026 | 10/07/2026 |

### Week 6 Achievements:

* Returned `risk_score`, `quality_score`, labels, decisions, reasons, and class probabilities.
* Blocked destructive commands and required review or blocking for sensitive-file changes.
* Produced end-to-end API evidence with a `require_review` decision.
* Documented the endpoint as a short-lived resource to redeploy after cleanup.
