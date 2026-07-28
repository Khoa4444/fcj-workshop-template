---
title: "Resource Cleanup"
date: 2026-07-28
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

#### Cleanup checklist

1. Clean up only after demo/evidence acceptance; retain Registry and Pipeline evidence required for the report.
2. Delete the SageMaker Endpoint, then its unused endpoint configuration.
3. Remove API Gateway, Lambda, and its role when the API is no longer needed.
4. Stop any future Model Monitor schedule; configure CloudWatch log retention and S3 lifecycle rules for temporary data.
5. Check for active Studio/notebook applications or Processing/Training jobs.
6. Retain `report/`, ARNs, and metrics needed for reporting before removing cloud data.

The demo endpoint was deleted to stop endpoint-hour charges. Check the current cloud state before another demo rather than relying on historical artifacts.

> **Image placeholder:** no remaining `agent-risk-scorer-endpoint` in SageMaker or CloudShell cleanup verification.
