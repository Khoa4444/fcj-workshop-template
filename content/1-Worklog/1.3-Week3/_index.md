---
title: "Week 3 Worklog"
date: 2026-06-15
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

* Extract trajectory features and create training datasets.
* Maintain a feature contract between preprocessing and inference.

### Tasks carried out this week:

| Day | Task | Start | Completion |
| --- | --- | --- | --- |
| Mon | Defined numeric, boolean, and source-indicator features. | 15/06/2026 | 15/06/2026 |
| Tue | Implemented `extract_features()` for JSONL trajectories. | 16/06/2026 | 16/06/2026 |
| Wed | Created file/tool/command counts, diff, test/lint, and safety-flag features. | 17/06/2026 | 17/06/2026 |
| Thu | Created stratified 70/15/15 train/validation/test splits. | 18/06/2026 | 18/06/2026 |
| Fri | Compared serving and preprocessing feature extractors. | 19/06/2026 | 19/06/2026 |

### Week 3 Achievements:

* Created 15 model features and CSV sets of 840 train, 180 validation, and 180 test records.
* Used `random_state=42` and stratified splitting for reproducibility.
* Identified `task_file_relevance_score` and `latency_total_ms` as proxies requiring real telemetry.
