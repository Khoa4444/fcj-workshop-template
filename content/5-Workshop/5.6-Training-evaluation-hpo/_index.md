---
title: "Managed Training, Evaluation, and HPO"
date: 2026-07-29
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

Validate local baseline/XGBoost training and test evaluation first. Then use the training notebook or the Pipeline for managed jobs. HPO maximizes validation macro F1 across two bounded trials; finalize it only after the tuning job is Completed. Recorded perfect results are synthetic-data evidence only.

