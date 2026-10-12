# Credit Card Fraud Detection

An end-to-end machine learning project exploring credit card fraud detection on a highly imbalanced dataset. The project compares XGBoost models, investigates SMOTE for minority-class oversampling, uses SHAP for explainability, tracks experiments with MLflow, and demonstrates data drift monitoring with Evidently AI.

## Problem Statement

Fraudulent transactions represent a very small proportion of credit card transactions. This class imbalance makes it difficult to evaluate a model using accuracy alone.

This project investigates how well an XGBoost classifier detects fraud and whether synthetic minority oversampling improves fraud detection recall.

## Objectives

- Explore the dataset and understand class imbalance.
- Train an XGBoost baseline classifier.
- Apply SMOTE to the training data and compare results.
- Evaluate models using precision, recall, F1 score, and PR-AUC.
- Explain model behaviour using SHAP.
- Track experiments with MLflow.
- Demonstrate feature drift monitoring with Evidently AI.

## Dataset

The original dataset contains 284,807 transactions and 31 columns.

- `Class`: target label (0 = legitimate, 1 = fraud).
- `Time` and `Amount`: transaction-related fields.
- `V1`–`V28`: PCA-transformed features.

Fraud accounts for approximately 0.17% of the original dataset.

## Methodology

1. **Exploratory Data Analysis:** Inspected data types, missing values, class distribution, and feature patterns.
2. **Baseline Model:** Trained XGBoost using the original imbalanced training data.
3. **Class Imbalance:** Applied SMOTE to the training set only and retrained XGBoost.
4. **Evaluation:** Compared precision, recall, F1 score, and PR-AUC on the same untouched test set.
5. **Explainability:** Used SHAP to rank features by their mean absolute contribution.
6. **Monitoring:** Used Evidently AI to compare reference data with a simulated production sample.
7. **Experiment Tracking:** Logged model parameters and evaluation metrics with MLflow.

## Results

| Metric | Baseline XGBoost | XGBoost + SMOTE |
|---|---:|---:|
| Precision | 1.0000 | 0.8947 |
| Recall | 0.7619 | 0.8095 |
| F1 score | 0.8649 | 0.8500 |
| PR-AUC | 0.9168 | 0.8877 |

### Key Findings

- The baseline achieved higher precision, F1 score, and PR-AUC.
- SMOTE increased recall from 76.19% to 80.95%.
- The recall improvement came with lower precision, illustrating the trade-off between catching fraud and producing false alerts.
- The baseline achieved the strongest F1 score among the two evaluated configurations.

These results apply to the test set used in this experiment and do not guarantee future or production performance.

## Explainability with SHAP

The top five features by mean absolute SHAP value were:

| Feature | Mean Absolute SHAP |
|---|---:|
| V4 | 1.3663 |
| V12 | 1.0231 |
| V14 | 0.6881 |
| V26 | 0.4734 |
| V2 | 0.4422 |

The features are PCA-transformed, so their original real-world meanings cannot be inferred from these importance values alone.

## Drift Monitoring with Evidently AI

A simulated production dataset was compared with the training reference data. The `Amount` feature was deliberately multiplied by 1.5 to demonstrate drift detection.

Evidently flagged one of 30 columns (3.33%) while the dataset-level drift condition remained negative under the configured threshold.

This was a controlled demonstration, not evidence of real production drift.

## Tech Stack

- Python
- Pandas and NumPy
- Scikit-learn
- XGBoost
- Imbalanced-learn (SMOTE)
- SHAP
- MLflow
- Evidently AI
- Matplotlib
- Google Colab

## Project Structure

```text
credit-card-fraud-detection/
├── README.md
├── MODEL_CARD.md
├── credit_card_fraud_detection.ipynb
├── data_drift_report.html
└── requirements.txt
```

The notebook filename and additional artifacts should be updated to match the files included in the final repository.

## Limitations

- Fraud is extremely rare in the dataset.
- The reported metrics depend on the selected test set and classification threshold.
- PCA-transformed features have limited direct interpretability.
- The drift experiment uses artificially modified data.
- Production security, scalability, latency, and operational performance have not been validated.

## Future Improvements

- Evaluate additional classifiers and tune decision thresholds.
- Validate performance on time-separated data.
- Monitor prediction quality when reliable fraud labels become available.
- Add automated testing and reproducible environment setup.
- Investigate deployment and production monitoring requirements.


