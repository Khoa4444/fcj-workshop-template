---
title: "Training, HPO, Registry và Pipeline"
date: 2026-07-28
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

#### Vòng đời model

`train_xgboost.py` huấn luyện `XGBClassifier` với `objective="multi:softprob"`; artifact gồm `xgboost_model.json` và `label_encoder.joblib`. Held-out evaluation dùng 180 simulator sample, ghi accuracy 1.0, macro F1 1.0, risky recall 1.0, false-negative rate 0.0. Đây chỉ là evidence trên synthetic rule-based scenario.

```powershell
python scripts/run_hpo.py --max-jobs 2 --max-parallel-jobs 1
python scripts/run_hpo.py --finalize <tuning-job-name>
python scripts/register_model.py
```

HPO tối ưu `validation:macro_f1`; artifact lịch sử ghi `max_depth=4`, `n_estimators=207`. Pipeline chạy `ProcessTrajectories → TrainXGBoost → EvaluateModel → CheckRiskyRecall (>=0.85) → RegisterModel`; execution `djsby9imdlsm` thành công, đăng ký version 2 `PendingManualApproval`. Endpoint không được deploy tự động.

> **Ảnh cần bổ sung:** Training metric, HPO best job, Model Registry version 2, Pipeline graph succeeded.
