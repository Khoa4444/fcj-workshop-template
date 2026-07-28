---
title: "Dữ liệu và SageMaker Processing"
date: 2026-07-28
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

#### Tạo dữ liệu và feature

```powershell
python data_generation/generate_scenarios.py --count 1200 --seed 42 --output data_generation/sample_trajectories.jsonl
(Get-Content data_generation/sample_trajectories.jsonl | Measure-Object -Line).Lines
python preprocessing/processing_script.py --input data_generation/sample_trajectories.jsonl --output-dir data/processed
aws s3 cp data_generation/sample_trajectories.jsonl s3://<ten-bucket>/raw/sample_trajectories.jsonl
python pipelines/sagemaker_pipeline.py --execute
```

Generator tạo 1.200 trajectory có sáu nhãn; Processing trích 15 feature và chia stratified 70/15/15 thành 840/180/180 record. `task_file_relevance_score` và `latency_total_ms` là proxy, không phải telemetry thực.

{{% notice note %}}Dữ liệu synthetic chỉ dùng chứng minh workflow; không dùng để tuyên bố production-ready. Log agent thật phải loại secret và được reviewer gán nhãn.{{% /notice %}}

> **Ảnh cần bổ sung:** generator 1.200 dòng, ba file split, S3 raw prefix và ProcessingStep/Pipeline succeeded.
