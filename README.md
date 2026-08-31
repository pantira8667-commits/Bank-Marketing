# Bank Marketing — Customer Subscription Prediction

## Project Overview

Machine Learning project for predicting whether a customer is likely to subscribe to a Term Deposit.

The goal is to support marketing teams in identifying customers with higher subscription potential and improving marketing campaign targeting.

## Business Objective

Develop a classification model that can help the Marketing team:

- Identify customers who are more likely to subscribe
- Prioritize high-potential customers
- Support customer targeting for marketing campaigns

## Prediction Target

| Class | Meaning |
|------|---------|
| no | Customer does not subscribe |
| yes | Customer subscribes |

## Dataset

The dataset contains customer information and marketing campaign information.

Total records: 45,211

### Train / Test Split

- Training Set: 36,168 samples
- Test Set: 9,043 samples
- Split Ratio: 80% / 20%
- random_state: 42

The training feature matrix contains 51 features after preprocessing, including numerical features and One-Hot Encoded categorical features.

## Machine Learning Workflow

```text
Dataset
   ↓
Data Quality Check
   ↓
Train / Test Split
   ↓
Data Preprocessing
   ├── Numerical Feature Scaling
   └── Categorical Feature Encoding
   ↓
Feature Matrix Construction
   ↓
Baseline Logistic Regression
   ↓
Model Evaluation
   ↓
Class Imbalance Handling
   ↓
Balanced Logistic Regression
   ↓
Probability Prediction
   ↓
Threshold Optimization
   ↓
SHAP Explainability
   ↓
Business Interpretation

## Model Performance

The model was evaluated using Precision, Recall, and F1-score.

### Baseline vs Balanced Logistic Regression

| Model | Recall (yes) | Precision (yes) |
|---|---:|---:|
| Baseline Logistic Regression | 0.34 | - |
| Balanced Logistic Regression | 0.83 | 0.42 |

The balanced model significantly improved Recall for the `yes` class from 0.34 to 0.83.

This improvement helps the model identify more customers who are likely to subscribe, although it comes with a trade-off in Precision.
