---
title: "Pipeline and Model Registry governance"
date: 2026-07-29
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

Upsert the Pipeline with `python pipelines/sagemaker_pipeline.py`; start billable execution only with `--execute`. Successful evaluation conditionally registers a PendingManualApproval package. Endpoint deployment is intentionally absent from the Pipeline.

