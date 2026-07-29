---
title: "Dataset step 4: Upload raw JSONL to S3"
date: 2026-07-29
weight: 4
chapter: false
pre: " <b> 5.4.4. </b> "
---

Upload `sample_trajectories.jsonl` to the recorded raw prefix `s3://agent-risk-scoring/raw/sample_trajectories.jsonl`. If your account cannot access the historical bucket, use your own bucket consistently through `.env` rather than silently changing source behavior.

