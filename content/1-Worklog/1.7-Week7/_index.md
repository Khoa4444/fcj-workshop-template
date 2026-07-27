---
title: "Week 7 Worklog"
date: 2026-07-13
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Establish inference observability and review monitoring limitations.
* Control costs after the demo.

### Tasks carried out this week:

| Day | Task | Start | Completion | Reference |
| --- | --- | --- | --- | --- |
| Mon | Enabled 100% endpoint data capture to S3. | 13/07/2026 | 13/07/2026 | `enable_data_capture.py` |
| Tue | Emitted `RiskScore` and `BlockedDecisions` metrics from Lambda to CloudWatch. | 14/07/2026 | 14/07/2026 | `lambda_handler.py` |
| Wed | Prepared the CloudWatch dashboard configuration. | 15/07/2026 | 15/07/2026 | `cloudwatch_dashboard.json` |
| Thu | Analyzed Default Model Monitor's flat-input requirement. | 16/07/2026 | 16/07/2026 | `model_monitor_config.py` |
| Fri | Reviewed endpoint, capture-data, and residual-resource cleanup. | 17/07/2026 | 17/07/2026 | `README.md` |

### Week 7 Achievements:

* Configured 100% S3 data capture, CloudWatch custom metrics, and a dashboard.
* Documented that Model Monitor scheduling needs flattening or a custom preprocessor for nested trajectory JSON.
* Identified endpoint deletion after the demo as necessary to avoid instance-hour costs.
