---
title: "Week 5 Worklog"
date: 2026-06-29
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

* Optimize the model and manage versions in Model Registry.
* Build an automated pipeline that registers only qualifying models.

### Tasks carried out this week:

| Day | Task | Start | Completion |
| --- | --- | --- | --- |
| Mon | Configured HPO with `validation:macro_f1` as the objective. | 29/06/2026 | 29/06/2026 |
| Tue | Reviewed the best job and selected hyperparameters. | 30/06/2026 | 30/06/2026 |
| Wed | Created the `agent-risk-scorer` model package group. | 01/07/2026 | 01/07/2026 |
| Thu | Designed a Pipeline with Processing, Training, Evaluation, and ConditionStep. | 02/07/2026 | 02/07/2026 |
| Fri | Set the default approval status to `PendingManualApproval`. | 03/07/2026 | 03/07/2026 |

### Week 5 Achievements:

* Captured HPO metadata with `max_depth=4` and `n_estimators=207`.
* Created the Model Registry package group and manual-approval mechanism.
* Registered a model only when risky recall met 0.85, separating registration from deployment.
