---
title: "Architecture and Objectives"
date: 2026-07-28
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

#### Problem and architecture

A final patch is insufficient to assess coding-agent safety. The workshop analyzes trajectories containing file operations, tools, commands, test/lint results, diffs, safety flags, and summaries.

```text
Mini Agent → JSON/JSONL → S3 → SageMaker Processing (15 features, 70/15/15)
→ XGBoost Training/HPO → Evaluation (risky_recall >= 0.85) → Model Registry
→ [manual release] Endpoint → Lambda → API Gateway POST /score-agent-run
Endpoint → S3 Data Capture; Lambda → CloudWatch RiskScore/BlockedDecisions
```

> **Image placeholder:** insert the project AWS architecture diagram here.

XGBoost fits tabular features; `risky_recall` is the quality gate; destructive commands are hard-blocked; deployment is separated from Pipeline; and Model Monitor requires flattened JSON or a custom preprocessor.
