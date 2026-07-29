---
title: "Step 1: Data and managed ML"
date: 2026-07-29
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---

The JSONL generator feeds Processing, which produces the three CSV splits. The Pipeline runs Processing, XGBoost training, evaluation, a `risky_recall >= 0.85` condition, and governed registration.

