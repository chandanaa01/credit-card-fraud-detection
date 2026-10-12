# Model Card: Credit Card Fraud Detection

## 1. Model Overview

- **Problem:** Credit card fraud detection
- **Model:** XGBoost Classifier
- **Experiment:** XGBoost with SMOTE
- **Experiment tracking:** MLflow
- **Explainability:** SHAP
- **Drift monitoring:** Evidently AI

This project demonstrates an end-to-end machine learning workflow
for detecting potentially fraudulent credit card transactions.

## 2. Intended Use

This model is intended for educational purposes, experimentation,
model evaluation, explainability, and monitoring demonstrations.

It is not a production-ready banking fraud prevention system.

## 3. Dataset

- Original dataset: 284,807 rows and 31 columns.
- Target: `Class` (0 = legitimate, 1 = fraud).
- Features include `Time`, `Amount`, and PCA-transformed
  features `V1` through `V28`.
- Fraud represents approximately 0.17% of the dataset.

## 4. Model Evaluation

| Metric | Baseline XGBoost | XGBoost + SMOTE |
|---|---:|---:|
| Precision | 1.0000 | 0.8947 |
| Recall | 0.7619 | 0.8095 |
| F1 score | 0.8649 | 0.8500 |
| PR-AUC | 0.9168 | 0.8877 |

The baseline achieved higher precision, F1 score, and PR-AUC.
The SMOTE model achieved higher recall.

These results apply to the evaluated test set and do not
guarantee performance on future transactions.

## 5. Explainability

The top five features by mean absolute SHAP value were:

1. `V4`: 1.3663
2. `V12`: 1.0231
3. `V14`: 0.6881
4. `V26`: 0.4734
5. `V2`: 0.4422

These are PCA-transformed features, so their original real-world
meanings cannot be inferred from their importance scores alone.

## 6. Drift Monitoring

Evidently AI detected drift in `Amount` after we deliberately
multiplied the simulated production values by 1.5.

One of 30 columns was flagged. This was an artificial experiment,
not evidence of drift in real production data.

## 7. Limitations and Risks

- Fraud cases are rare and the dataset is imbalanced.
- False negatives can allow fraudulent transactions to go undetected.
- False positives can inconvenience legitimate customers.
- Fraud patterns can change over time.
- Evaluation results may not generalize to other datasets or banks.
- SHAP explains model behaviour but does not establish causation.
- Production security, latency, scalability, and operational
  performance have not been validated.

## 8. Ethical and Regulatory Considerations

Fraud detection can affect customers through transaction declines,
account restrictions, and additional verification.

A real deployment would require privacy safeguards, monitoring,
human review, and a process for handling disputed decisions.

The EU AI Act classification depends on the system's intended
purpose and applicable provisions. This educational prototype
is not a legal compliance assessment.

## 9. Future Work

- Evaluate additional models and classification thresholds.
- Validate performance on time-separated data.
- Monitor precision, recall, false-positive rates, and feature drift.
- Test security, scalability, and latency before deployment.
- Establish a human review and escalation process.

## 10. Project Status

**Educational prototype — not approved for production use.**
