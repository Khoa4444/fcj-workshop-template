---
title: "Kiến trúc bước 1: Data và managed ML"
date: 2026-07-29
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---

## Data path

`data_generation/generate_scenarios.py` tạo `sample_trajectories.jsonl`. Mỗi record được `processing_script.py` biến thành 15 feature và split thành `train.csv`, `validation.csv`, `test.csv`.

## Managed ML path

Pipeline nhận input mặc định:

```text
s3://agent-risk-scoring/raw/sample_trajectories.jsonl
```

Nó khởi tạo `SKLearnProcessor(framework_version="1.2-1")`, sau đó `SKLearn` estimator chạy `training/train_xgboost.py`. `EvaluateModel` giải nén `model.tar.gz`, cài `xgboost==2.1.4`, đánh giá test split, và xuất `evaluation.json`. `ConditionGreaterThanOrEqualTo` chỉ register khi `risky_recall >= 0.85`.

> **[ẢNH PLACEHOLDER — Pipeline graph]** SageMaker Console → Pipelines → `agent-risk-scorer-pipeline` → Graph. Cần thấy năm node Process, Train, Evaluate, Check, Register.

