---
title: "Managed Training, Evaluation và HPO"
date: 2026-07-29
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

## Local training và evaluation

Trước managed run, xác minh source code local:

```powershell
python training/train_sklearn.py `
  --train data/processed/train.csv `
  --validation data/processed/validation.csv `
  --model-dir models

python training/train_xgboost.py `
  --train data/processed/train.csv `
  --validation data/processed/validation.csv `
  --model-dir models

python training/evaluate_model.py `
  --test data/processed/test.csv `
  --model-dir models `
  --output models/evaluation_report.json
Get-Content models/evaluation_report.json
```

## Managed Training

Trong cửa sổ Jupyter đã mở ở 5.5, mở `notebooks/03_training_experiments.ipynb`, chọn cùng kernel `.venv` và chạy từng cell theo thứ tự.

- Các cell đầu tạo `TrainingInput` từ `s3://$bucket/processed/train.csv` và `validation.csv`.
- Cell baseline chạy `training/train_sklearn.py` trên `ml.m5.large` với `wait=True`, `logs=True`.
- Cell XGBoost chạy `training/train_xgboost.py` trên `ml.m5.large`; XGBoost dependency nằm trong `training/requirements.txt`.
- Cell verify gọi `describe_training_job` và assert cả hai job `Completed`.

Chỉ chạy cell HPO sau khi baseline/XGBoost completed. Không chạy notebook từ thư mục `notebooks/`, vì nó cần repository root làm working directory.

## HPO

HPO objective là `validation:macro_f1`; search gồm `max_depth`, `learning_rate`, `n_estimators`, `subsample`, `colsample_bytree`. Khởi chạy tối đa 2 trial theo script:

```powershell
python scripts/run_hpo.py --max-jobs 2 --max-parallel-jobs 1
```

Sau khi Console báo job `Completed`, tìm job mới nhất và ghi report:

```powershell
$tuningJob = aws sagemaker list-hyper-parameter-tuning-jobs --region ap-southeast-1 --sort-by CreationTime --sort-order Descending --query "HyperParameterTuningJobSummaries[?starts_with(HyperParameterTuningJobName, 'agent-risk-xgb-hpo')].HyperParameterTuningJobName | [0]" --output text
python scripts/run_hpo.py --finalize $tuningJob
Get-Content report/best_model_metrics.json
```

Sau khi finalize thành công, `report/best_model_metrics.json` là input bắt buộc của `scripts/register_model.py` ở bước 5.7. Không deploy endpoint khi file này chưa được cập nhật bởi chính HPO run hiện tại.

Recorded HPO job historical `agent-risk-xgb-hpo-260723-2011` selected `max_depth=4`, `n_estimators=207`, learning rate khoảng `0.1452`; recorded validation metrics là 1.0 trên synthetic data. Kết quả live mới có thể khác.

> **[ẢNH PLACEHOLDER — completed XGBoost training]** SageMaker Console → Training jobs → XGBoost job vừa tạo. Ảnh phải thấy `Completed`, `ml.m5.large`, input train/validation và phần logs có `validation:risky_recall`. Không đặt HPO chart trong ảnh này.

> **[ẢNH PLACEHOLDER — completed HPO]** SageMaker Console → Hyperparameter tuning jobs → job mới nhất. Ảnh phải thấy objective `validation:macro_f1`, status `Completed` và best training job. Đây là ảnh riêng cho HPO.

> **[ẢNH PLACEHOLDER — HPO artifact report]** Mở `report/best_model_metrics.json` vừa được tạo. Ảnh phải thấy `tuning_job_name`, `best_training_job_name`, hyperparameters và metrics; che account-specific S3 URI nếu cần công khai.

