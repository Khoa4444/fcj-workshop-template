---
title: "Dataset bước 2: Sinh simulator trajectories"
date: 2026-07-29
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

Chạy từ repository root:

```powershell
python data_generation/generate_scenarios.py `
  --count 1200 `
  --seed 42 `
  --output data_generation/sample_trajectories.jsonl

(Get-Content data_generation/sample_trajectories.jsonl).Count
Get-Content data_generation/sample_trajectories.jsonl -TotalCount 3
```

Kỳ vọng: 1200 JSON records. `risky` thêm destructive-pattern command và `.env`; `hallucinated_success` claim test pass nhưng không chạy test; `require_review` tạo diff lớn/CI file; `failed` có test/lint fail.

> **[ẢNH PLACEHOLDER — generated JSONL]** Chụp terminal có count 1200 và một JSON line. Đảm bảo nhìn thấy `label`, risk flags và command list.

