---
title: "Tired of Manual Hyperparameter Tuning? Try SageMaker Automatic Model Tuning"
date: 2026-07-30
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

## Post details

| Information | Details |
|---|---|
| Publication date | Pending approval |
| Status | Pending approval |
| Platform | AWS Study Group - Facebook Group |
| Facebook link | Pending approval |

![Model-training flow with Amazon SageMaker](/images/3-BlogsPosted/sagemaker-automatic-model-tuning.png)

*Figure 1. Amazon SageMaker creates a Training Job from a notebook, uses data in Amazon S3, stores model artifacts in S3, and sends logs and metrics to Amazon CloudWatch.*

Machine-learning work has a stage that can easily consume an endless amount of time: the model can already train and the data may be sound, yet it is still unclear which learning rate, maximum depth, or regularization settings will produce better results.

Trying a few settings manually is simple. But as the number of hyperparameters grows, the number of possible combinations increases rapidly. Running each experiment and recording it by hand is not only time-consuming; it also makes it difficult to know whether a stronger configuration has been missed.

Amazon SageMaker Automatic Model Tuning (AMT) is designed to address this problem.

Instead of creating many training jobs manually, I only need to prepare three things:

* **Training job:** the model or algorithm to train, such as XGBoost.
* **Objective metric:** the metric to optimize, such as `validation:accuracy`, macro F1, or risky recall.
* **Search space:** the ranges of hyperparameter values to explore.

SageMaker AMT then creates multiple trials automatically. Each trial is a SageMaker Training Job with a different hyperparameter configuration. When the process finishes, I can inspect the best trial, the model it produced, its logs, and the hyperparameter values that were used.

## An XGBoost search-space example

For XGBoost, AMT can explore ranges such as:

* `eta` (learning rate): 0.1 to 0.5.
* `alpha` (L1 regularization): 0.01 to 0.5.
* `max_depth`: 1 to 10.
* `min_child_weight`: 0 to 2.

The important point is not to take the best trial and stop there. The more interesting part is examining the full set of results.

If trials with `eta` near 0.5 often produce stronger metrics, the next run can expand that range for further exploration. If `max_depth` works well only at a few values, the search space can be narrowed to avoid spending trials on weak configurations. HPO therefore does more than select one good set of values: it also helps reveal which hyperparameters the model is sensitive to.

In SageMaker, trials can be viewed in the console like ordinary training jobs: hyperparameters, input data, run time, CloudWatch logs, and metrics all have a history. This is useful when comparing trials or explaining why a particular model was selected.

## Applying it to the AI Agent Risk Scorer

For the AI Agent Risk Scorer project, this is especially important: optimization should not focus only on accuracy. If the goal is to reduce missed dangerous trajectories, risky recall or the risky false-negative rate represents risk more directly. Selecting the right objective metric matters as much as running many trials.

Finally, HPO has a cost because every trial is a training job. It is best to start with a well-grounded search space, limit the number of trials with `max_jobs`, monitor the results, and then run the next iteration with a more focused range. After selecting a strong model, evaluation, model registry, approval, and monitoring are still required before production deployment.

In short, SageMaker AMT does not replace ML reasoning, but it turns “trying each hyperparameter set manually” into a process that is systematic, measurable, and easier to repeat.

## References

- [Optimize hyperparameters with Amazon SageMaker Automatic Model Tuning — AWS](https://aws.amazon.com/blogs/machine-learning/optimize-hyperparameters-with-amazon-sagemaker-automatic-model-tuning/)
- [Explore advanced techniques for hyperparameter optimization with SageMaker AMT — AWS](https://aws.amazon.com/blogs/machine-learning/explore-advanced-techniques-for-hyperparameter-optimization-with-amazon-sagemaker-automatic-model-tuning/)
- [Perform Automatic Model Tuning with SageMaker — AWS Documentation](https://docs.aws.amazon.com/sagemaker/latest/dg/automatic-model-tuning.html)

---

[Back to Blogs Posted](../)
