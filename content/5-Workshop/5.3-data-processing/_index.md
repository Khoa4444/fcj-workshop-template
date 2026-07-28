---
title: "Data and SageMaker Processing"
date: 2026-07-28
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

#### Generate data and features

```powershell
python data_generation/generate_scenarios.py --count 1200 --seed 42 --output data_generation/sample_trajectories.jsonl
python preprocessing/processing_script.py --input data_generation/sample_trajectories.jsonl --output-dir data/processed
aws s3 cp data_generation/sample_trajectories.jsonl s3://<bucket-name>/raw/sample_trajectories.jsonl
python pipelines/sagemaker_pipeline.py --execute
```

The generator creates 1,200 trajectories across six labels. Processing extracts 15 features and creates stratified 70/15/15 splits of 840/180/180 records. `task_file_relevance_score` and `latency_total_ms` are proxies, not real telemetry.

{{% notice note %}}Synthetic data proves the workflow only; it is not production readiness evidence. Real agent logs require secret removal and reviewer labels.{{% /notice %}}

> **Image placeholder:** 1,200-record generation, splits, S3 raw prefix, and successful ProcessingStep/Pipeline.
