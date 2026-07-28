---
title: "Training, HPO, Registry, and Pipeline"
date: 2026-07-28
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

#### Model lifecycle

`train_xgboost.py` trains an `XGBClassifier` using `objective="multi:softprob"` and produces `xgboost_model.json` plus `label_encoder.joblib`. Held-out evaluation on 180 simulator samples recorded accuracy 1.0, macro F1 1.0, risky recall 1.0, and a 0.0 false-negative rate; these are synthetic rule-based results only.

```powershell
python scripts/run_hpo.py --max-jobs 2 --max-parallel-jobs 1
python scripts/run_hpo.py --finalize <tuning-job-name>
python scripts/register_model.py
```

HPO optimizes `validation:macro_f1`; historical output has `max_depth=4` and `n_estimators=207`. Pipeline: `ProcessTrajectories → TrainXGBoost → EvaluateModel → CheckRiskyRecall (>=0.85) → RegisterModel`. Execution `djsby9imdlsm` succeeded and registered version 2 as `PendingManualApproval`; endpoint release is manual.

> **Image placeholder:** training metrics, HPO best job, Registry version 2, and successful Pipeline graph.
