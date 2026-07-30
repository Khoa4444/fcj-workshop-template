---
title: "Self-Assessment"
date: 2026-07-30
weight: 6
chapter: false
pre: " <b> 6. </b> "
---

## Overview

During my internship from **01/06/2026 to 23/08/2026** at **Amazon Web Services Viet Nam Company Limited**, I participated in the **Workforce Bootcamp – First Cloud AI Journey**. My main work was to build and document the **AI Coding Agent Risk Scorer**: a system that records coding-agent trajectories, extracts features, evaluates risk with an ML model, and applies a policy to allow, require review, or block a run.

The work connected my Computer Science background with practical AWS and MLOps experience. I completed an eight-week worklog, project proposal, technical workshop, specialist blog posts, event reports, and bilingual project documentation. More importantly, I learned that a useful AI system needs more than a model with good metrics: it also needs suitable data, evaluation processes, governance, monitoring, cost controls, and human involvement in high-risk decisions.

## Outcomes and skills gained

- Built a data workflow for AI Coding Agent Risk Scorer from JSON/JSONL trajectories and feature engineering through data splitting, XGBoost training, and evaluation.
- Developed a clearer understanding of Amazon S3, SageMaker Processing, Training, HPO, Pipelines, Model Registry, Endpoint, Lambda, API Gateway, CloudWatch, and Model Monitor in an ML workflow.
- Practiced governance-oriented design through quality gates, manual approval, decision policies, false-negative control, and the distinction between a registered model and a deployed model.
- Improved my ability to read AWS documentation, analyze architectures, write technical documentation, collect evidence, and present project content bilingually.
- Strengthened self-learning through AWS Cloud Practitioner, SLA/monitoring, web-application security, Agentic AI, and the practical projects presented at events.

## Assessment by criterion

| No. | Criterion | Self-assessment | Basis for assessment |
| --- | --- | --- | --- |
| 1 | Professional knowledge and technical skills | Fair | Applied Python, ML/XGBoost, AWS, and MLOps to complete a workflow covering data, training, evaluation, governance, and monitoring. |
| 2 | Learning ability | Good | Proactively learned AWS services, MLOps concepts, and the limitations of synthetic data. |
| 3 | Proactiveness | Good | Completed project documentation, workshop, blog posts, and evidence; proactively checked report content, links, and images. |
| 4 | Responsibility | Good | Tracked work through the worklog, maintained documentation structure, and cleaned up demo resources that could incur cost. |
| 5 | Discipline and time management | Fair | Completed the main milestones; I still need to estimate time more accurately for testing, documentation, and final review. |
| 6 | Problem-solving | Good | Analyzed issues through evidence, separated technical causes from data limitations, and prioritized verifiable solutions. |
| 7 | Communication and presentation | Fair | Can consolidate technical work into a proposal, workshop, and blog posts; I need more practice presenting concisely to a team or review panel. |
| 8 | Collaboration and feedback | Fair | Participated in FCAJ activities, learned from speakers, and adjusted documentation to report requirements. |
| 9 | Security and cost awareness | Fair | Recognized least privilege, secret management, manual approval, Endpoint/API cleanup, and the need not to overstate synthetic metrics. |
| 10 | Contribution to the project | Good | Completed a report set traceable from worklog and proposal through workshop, blog posts, evidence, and technical documentation. |
| 11 | Overall | Good | Achieved the learning and prototype-building objectives with a clear MLOps workflow; I still need to expand real-world data and production-deployment experience. |

## Areas for improvement

1. **Real-world data and evaluation:** The current dataset is mostly synthetic. I need deeper experience in collecting representative data, obtaining independent labels, evaluating distribution shift, and designing more reliable experiments.
2. **Production deployment and security:** I need to develop further in least-privilege IAM, multi-account operations, CI/CD, observability, and cost optimization for long-running services.
3. **Technical communication:** I need more practice presenting architecture, explaining trade-offs, and defending technical decisions clearly and concisely to both technical and non-technical audiences.

## Next steps

After the program, I will continue developing cloud and AI/ML expertise through AWS hands-on practice, stronger system-design foundations, and small projects that include monitoring, security, and cost awareness from the start. For AI Coding Agent Risk Scorer, the appropriate next step is to add real trajectories with human labels, re-evaluate the model on more representative data, and move toward production only after completing suitable governance controls.
