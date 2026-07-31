---
title: "Optimize Hyperparameters with SageMaker Automatic Model Tuning"
date: 2026-07-30
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

## Post details

| Information | Details |
|---|---|
| Publication date | 31/07/2026 |
| Status | Published |
| Platform | AWS Study Group - Facebook Group |
| Facebook link | [View post](https://www.facebook.com/share/p/1GvynuCYcp/) |

![Model-training flow with Amazon SageMaker](/images/3-BlogsPosted/sagemaker-automatic-model-tuning.png)

*Figure 1. Amazon SageMaker creates a Training Job from a notebook, uses data in Amazon S3, stores model artifacts in S3, and sends logs and metrics to Amazon CloudWatch.*

# Optimize Hyperparameters with Amazon SageMaker Automatic Model Tuning: letting the model find its “sweet spot”

A good machine-learning model does not come only from clean data or a suitable algorithm. One small configuration layer can have a major effect on the final result: **hyperparameters**.

For example, when training XGBoost, we need to decide the learning rate, maximum tree depth, regularization coefficients, and number of training rounds. These are not parameters that the model learns directly from the data. They are the “knobs” an ML practitioner sets before learning begins. If they are not chosen appropriately, the model can learn slowly, overfit, or deliver lower accuracy than expected.

The difficulty is that the hyperparameter-combination space is often very large. Trying every configuration manually is time-consuming, hard to reproduce, and quickly becomes costly when each trial requires training infrastructure to be provisioned.

This is where **Amazon SageMaker Automatic Model Tuning (AMT)** becomes useful.

## What does AMT do?

Instead of manually coordinating dozens of experiments, an ML practitioner only needs to prepare three things:

- A training job.
- An objective metric to optimize, such as validation accuracy.
- A range of values to explore for each hyperparameter.

SageMaker AMT then creates and orchestrates training jobs, tracks metrics, compares results, and finds stronger hyperparameter combinations. SageMaker manages the training infrastructure, containers, logs, model artifacts, and experiment history.

## An XGBoost example

In an AWS hands-on example, an XGBoost model is used to classify handwritten digits from 0 to 9. Training and validation data are uploaded to Amazon S3; SageMaker uses a ready-made XGBoost image, provisions training resources, and saves the model when the run completes.

At first, we can run one training job to validate the pipeline. Next, rather than fixing every value, we define ranges to search, for example:

- `alpha`: 0.01 to 0.5.
- `eta` (learning rate): 0.1 to 0.5.
- `min_child_weight`: 0 to 2.
- `max_depth`: integer values from 1 to 10.

AMT samples different combinations in this space, runs the model, and measures `validation:accuracy`. With accuracy as the objective to maximize, each run becomes a documented experiment rather than a guess at which settings may work.

## Why is the Bayesian strategy notable?

This example uses a **Bayesian** search strategy. Its strength is that later trials can use the results of earlier trials to prioritize promising regions of the hyperparameter space.

In the demonstration, 50 trials were performed with up to three jobs running in parallel. The best trial achieved approximately **89.815%** validation accuracy. The important value, however, is not only the “best configuration.” By visualizing all trials, we can also identify trends:

- `eta` values near the upper end of the tested range produced better results than values near 0.
- `alpha` showed the opposite tendency.
- `max_depth` performed well only in certain value ranges.

These observations help an ML team go beyond a temporary optimum. The team can narrow or expand the search ranges for the next optimization cycle and gain a clearer understanding of which hyperparameters the model is sensitive to.

## Practical lessons

Hyperparameter tuning should not be treated as a secondary step after a model already exists. It is part of a disciplined ML-development process:

1. Select a metric that accurately reflects the business or technical objective.
2. Start with a search range based on an understanding of the algorithm.
3. Track every trial, its cost, and its training logs.
4. Visualize results to learn from both strong and weak regions.
5. Refine the search space in subsequent iterations.

SageMaker AMT does not replace ML reasoning. It reduces repetitive operational and experimentation work so we can focus on more important decisions: whether the data are good enough, whether the metric is appropriate, whether the proposed ranges are reasonable, and what the model is actually learning.

If you are using AWS to build a machine-learning pipeline, AMT is worth considering as a way to turn manual “knob turning” into a systematic, observable, and scalable process.

## References

- [Optimize hyperparameters with Amazon SageMaker Automatic Model Tuning — AWS](https://aws.amazon.com/blogs/machine-learning/optimize-hyperparameters-with-amazon-sagemaker-automatic-model-tuning/)
- [Explore advanced techniques for hyperparameter optimization with SageMaker AMT — AWS](https://aws.amazon.com/blogs/machine-learning/explore-advanced-techniques-for-hyperparameter-optimization-with-amazon-sagemaker-automatic-model-tuning/)
- [Perform Automatic Model Tuning with SageMaker — AWS Documentation](https://docs.aws.amazon.com/sagemaker/latest/dg/automatic-model-tuning.html)

---

[Back to Blogs Posted](../)
