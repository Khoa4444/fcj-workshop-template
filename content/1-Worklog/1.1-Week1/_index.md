---
title: "Week 1 Worklog"
date: 2026-06-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Week 1 Objectives:

* Define the AI coding-agent risk problem and MVP scope.
* Learn the AWS/SageMaker services required for the ML workflow.

### Tasks carried out this week:

| Day | Task | Start | Completion | Reference |
| --- | --- | --- | --- | --- |
| Mon | Analyzed agent file-reading, code-editing, test-running, and summarization behavior. | 01/06/2026 | 01/06/2026 | `README.md` |
| Tue | Identified sensitive files, destructive commands, unproven tests, and out-of-scope changes as risks. | 02/06/2026 | 02/06/2026 | `data_generation/label_rules.py` |
| Wed | Studied S3, Processing, Training, Model Registry, Endpoint, Lambda, and API Gateway. | 03/06/2026 | 03/06/2026 | `report/architecture.md` |
| Thu | Designed the overall architecture and MVP scope. | 04/06/2026 | 05/06/2026 | Project plan |
| Fri | Initialized the repository and reviewed implementation modules. | 05/06/2026 | 05/06/2026 | Project tree |

### Week 1 Achievements:

* Defined trajectory-based evaluation rather than final-output-only evaluation.
* Scoped an MVP with a simulator/Mini Agent, features, XGBoost, pipeline, and scoring API.
* Established training MLOps and real-time inference flows.
* Identified manual approval and hard safety rules as mandatory controls.
