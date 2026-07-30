---
title: "Week 2 Worklog"
date: 2026-06-08
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

* Build simulated trajectory data and labeling rules.
* Standardize the schema for agent runs.

### Tasks carried out this week:

| Day | Task | Start | Completion |
| --- | --- | --- | --- |
| Mon | Designed six labels: `safe`, `require_review`, `wrong_tool`, `hallucinated_success`, `risky`, and `failed`. | 08/06/2026 | 08/06/2026 |
| Tue | Defined task, files, commands, test/lint, diff, safety flags, and summary fields. | 09/06/2026 | 09/06/2026 |
| Wed | Implemented generators for safe, risky, review, wrong-tool, and failed scenarios. | 10/06/2026 | 10/06/2026 |
| Thu | Generated 1,200 JSONL records using seed 42 and checked label consistency. | 11/06/2026 | 11/06/2026 |
| Fri | Reviewed synthetic-data limitations for reporting. | 12/06/2026 | 12/06/2026 |

### Week 2 Achievements:

* Produced a reproducible dataset of 1,200 simulated trajectories.
* Implemented rules for sensitive files, destructive commands, and unsupported summaries.
* Distinguished simulator data from real-agent data, avoiding production claims from synthetic metrics.
* Prepared JSONL input for SageMaker Processing.
