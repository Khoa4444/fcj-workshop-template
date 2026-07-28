---
title: "Proposal"
date: 2026-07-28
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# AI Coding Agent Risk Scorer on AWS SageMaker

## 1. Project Overview

AI Coding Agent Risk Scorer evaluates the risk of each AI coding-agent execution. Rather than examining only the final patch or answer, it retains a **trajectory log** containing file operations, tools, commands, test/lint results, diff size, sensitive-file signals, and the agent summary.

Trajectories are transformed into tabular features. An XGBoost model predicts an operational label, `risk_score`, and `quality_score`; a decision policy combines model output with hard safety rules to return `allow`, `require_review`, or `block`.

The project uses Amazon S3, SageMaker Processing, Training, HPO, Model Registry, Pipelines, Endpoint, AWS Lambda, API Gateway, CloudWatch, and S3 Data Capture. The pipeline has completed successfully and registered model package version 2 with `PendingManualApproval` status.

## 2. Objectives

1. Standardize trajectory logs for coding-agent runs.
2. Generate labeled simulated data and extract features with SageMaker Processing.
3. Train and evaluate a multiclass XGBoost model, then optimize hyperparameters.
4. Use `risky_recall` as a quality gate before Model Registry registration.
5. Provide `POST /score-agent-run` for trajectory scoring.
6. Block destructive commands and review sensitive behavior through rule-based guardrails.
7. Capture inference data in S3 and custom metrics in CloudWatch.
8. Retain manual approval and separate training/registration from endpoint release.

## 3. Problem Statement

The final output of an AI coding agent does not show whether its execution was safe. Risks include out-of-scope changes; access to `.env`, secrets, credentials, CI/CD, or deployment configuration; destructive commands; unsupported test-pass claims; and large diffs requiring review.

The system classifies trajectories as `safe`, `require_review`, `wrong_tool`, `hallucinated_success`, `risky`, or `failed`. ML estimates risk probabilities, while policy guardrails handle clearly dangerous behavior without relying solely on model predictions.

## 4. Solution Architecture

Processing flow: **Mini Coding Agent/Agent Runner → Trajectory JSON/JSONL → Amazon S3 → SageMaker Processing (15 features, 70/15/15 split) → SageMaker Training/HPO → Model Registry → Endpoint → Lambda → API Gateway → Client/Demo CLI**.

SageMaker Pipelines automate **Processing → Training → Evaluation → CheckRiskyRecall → RegisterModel**. Endpoint deployment is a separate release step. Monitoring consists of Endpoint → S3 Data Capture and Lambda → CloudWatch custom metrics/dashboard.

> **Image placeholder 1 — Overall architecture:** to be added at `/images/2-Proposal/architecture-overview.png`.

> **Image placeholder 2 — MLOps and inference flow:** to be added at `/images/2-Proposal/mlops-inference-flow.png`.

| Component | Responsibility |
| --- | --- |
| Mini Agent | Produces trajectories from file reads/edits and test execution |
| S3 | Stores raw trajectories, processed CSVs, artifacts, reports, and capture data |
| SageMaker Processing | Extracts 15 features and creates 70/15/15 splits |
| SageMaker Training/HPO | Trains and optimizes XGBoost using `validation:macro_f1` |
| Pipeline/Registry | Enforces `risky_recall >= 0.85` and registers models pending approval |
| Endpoint/Lambda/API Gateway | Provides `POST /score-agent-run` real-time inference |
| CloudWatch/S3 Data Capture | Records `RiskScore`, `BlockedDecisions`, and inference evidence |

## 5. Timeline

| Week | Main work | Deliverable | Status |
| --- | --- | --- | --- |
| 1 | Risk analysis, MVP, architecture | Architecture, repository skeleton | Complete |
| 2 | Generator, schema, label rules | 1,200-record JSONL dataset | Complete |
| 3 | Feature engineering and data split | Train/validation/test CSVs | Complete |
| 4 | XGBoost and held-out evaluation | Model artifact, metrics | Complete |
| 5 | HPO, Registry, Pipeline | HPO metadata, model package | Complete |
| 6 | Endpoint, Lambda/API Gateway, API demo | Serving/API evidence | Redeploy required for another demo |
| 7 | Data capture and CloudWatch | Monitoring configuration | Partially complete |
| 8 | Report, worklog, roadmap | Documentation/evidence | Complete |

## 6. Risks and Mitigations

| Risk | Impact | Mitigation |
| --- | --- | --- |
| Synthetic data is not representative | High | Collect real trajectories and human labels; do not claim production performance |
| Missed `risky` run | High | Risky-recall gate and false-negative monitoring |
| Dangerous agent operation | High | Tool policy and hard `block` rule |
| Training-serving feature drift | Medium | Shared feature package and contract/regression tests |
| Model Monitor cannot process nested JSON | Medium | Flatten payload or apply a custom preprocessor |
| Continuous endpoint cost | Medium | Deploy only for demos and clean up afterward |
| IAM/API not production-grade | High | Audit IAM policies, authentication, and rate limiting |

## 7. Internal References

`README.md`, `report/architecture.md`, `report/pipeline_execution.json`, `report/best_model_metrics.json`, `report/model_registry.json`, `report/endpoint_deployment.json`, `report/api_gateway.json`, `report/monitoring_setup.json`.
