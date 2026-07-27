---
title: "Week 4 Worklog"
date: 2026-06-22
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

* Train and evaluate the risk-classification model.
* Define a safety metric as the quality gate.

### Tasks carried out this week:

| Day | Task | Start | Completion | Reference |
| --- | --- | --- | --- | --- |
| Mon | Built a multiclass XGBoost training script and LabelEncoder. | 22/06/2026 | 22/06/2026 | `train_xgboost.py` |
| Tue | Saved the model and encoder as inference artifacts. | 23/06/2026 | 23/06/2026 | `xgboost_model.json` |
| Wed | Implemented held-out test-set evaluation. | 24/06/2026 | 24/06/2026 | `evaluate_pipeline.py` |
| Thu | Evaluated accuracy, macro F1, risky recall, and risky false-negative rate. | 25/06/2026 | 25/06/2026 | `evaluation_report.json` |
| Fri | Selected `risky_recall >= 0.85` as the quality gate. | 26/06/2026 | 26/06/2026 | `sagemaker_pipeline.py` |

### Week 4 Achievements:

* Built a `multi:softprob` multiclass XGBoost classifier and evaluated 180 simulator samples.
* Recorded accuracy 1.0, macro F1 1.0, risky recall 1.0, and a 0.0 false-negative rate.
* Clarified that perfect metrics validate the synthetic workflow, not production performance.
