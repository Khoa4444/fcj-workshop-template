---
title: "Dataset bước 1: Data contract và feature schema"
date: 2026-07-29
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

Mở `preprocessing/feature_schema.json`. Schema định nghĩa 7 numeric feature, 6 boolean feature, 1 categorical source và target `label`. Trong CSV thực tế, source được one-hot thành `source_simulator` và `source_mini_llm_agent`, vì vậy model input có 15 cột.

```powershell
Get-Content preprocessing/feature_schema.json
Get-Content data/processed/train.csv -TotalCount 2
```

`task_file_relevance_score` hiện là hằng số giả lập `0.85`; `latency_total_ms` được suy ra bằng số tool × 150. Đây là giới hạn cần ghi rõ khi trình bày.

> **[ẢNH PLACEHOLDER — schema]** Chụp `feature_schema.json` và header `train.csv` trong VS Code. Đánh dấu `label` chỉ xuất hiện trong training CSV, không trong endpoint input.

