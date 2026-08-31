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

  text
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

## Data Preparation & Model Development

The dataset was first checked for data quality before being split into training and test sets using an 80/20 ratio.

Numerical features were scaled using `StandardScaler`, while categorical features were transformed using `OneHotEncoder`.

The preprocessing steps were fitted using the training data and then applied to the test data to help prevent data leakage.

After preprocessing, the training feature matrix contained 51 features.

Logistic Regression was selected as the baseline classification model.

Because the target variable was imbalanced, a second Logistic Regression model was trained using `class_weight="balanced"` to give greater importance to the minority `yes` class.

## Model Evaluation & Class Imbalance

The models were evaluated using Accuracy, Precision, Recall, F1-score, and Confusion Matrix.

### Model Comparison

| Metric | Baseline | Balanced |
|---|---:|---:|
| Accuracy | 0.90 | 0.84 |
| Precision (`yes`) | 0.65 | 0.42 |
| Recall (`yes`) | 0.34 | 0.83 |
| F1-score (`yes`) | 0.45 | 0.56 |

The baseline model achieved an Accuracy of 0.90, but Recall for the `yes` class was only 0.34.

After applying `class_weight="balanced"`, Recall for the `yes` class increased from 0.34 to 0.83, while F1-score increased from 0.45 to 0.56.

However, Accuracy decreased from 0.90 to 0.84, while Precision for the `yes` class decreased from 0.65 to 0.42.

This demonstrates why Accuracy alone is not sufficient when evaluating an imbalanced classification problem.

## Probability & Threshold Analysis

The Balanced Logistic Regression model was used with `predict_proba()` to obtain the probability of each class.

The test set contained 9,043 observations and two classes:

`['no', 'yes']`

Therefore:

- `y_prob[:, 0]` → Probability of `no`
- `y_prob[:, 1]` → Probability of `yes`

The predicted probability of `yes` can be used to rank customers according to their likelihood of subscribing.

Different classification thresholds were explored to understand the trade-off between Precision, Recall, and F1-score.

The selected model was Balanced Logistic Regression with a classification threshold of 0.5.

The threshold was selected based on the performance of the `yes` class, particularly Recall, Precision, and F1-score.

## SHAP Explainability

SHAP was used to understand which features had the greatest influence on model predictions.

The analysis showed that `duration` was the most influential feature.

Other influential features included:

- `contact`
- `month`
- `poutcome`
- `campaign`

SHAP provides model interpretability by showing how features contribute to predictions.

## Business Interpretation

The business objective is to identify customers who are more likely to subscribe to a Term Deposit and use this information to support marketing campaign targeting.

The Balanced Logistic Regression model improves the ability to identify potential subscribers by increasing Recall for the `yes` class.

The predicted probability can also be used to rank customers and prioritize those with higher subscription potential.

This could help marketing teams allocate campaign resources more effectively instead of treating all customers equally.

However, the model should be used as a decision-support tool rather than a replacement for business judgment.

## Project Summary

This project demonstrates an end-to-end Machine Learning workflow for customer subscription prediction.

The project covers:

- Data quality checking
- Train / test splitting
- Numerical feature scaling
- Categorical feature encoding
- Feature matrix construction
- Logistic Regression
- Class imbalance handling
- Model evaluation
- Probability prediction
- Threshold optimization
- SHAP explainability
- Business interpretation

The key result was that the Balanced Logistic Regression model increased Recall for potential subscribers from 0.34 to 0.83 and improved F1-score from 0.45 to 0.56.

Although the balanced model achieved lower overall Accuracy and Precision, it was substantially better at identifying customers who actually subscribed.

## Limitations

- The dataset contains significant class imbalance.
- The Balanced model has relatively low Precision for the `yes` class.
- Improving Recall can reduce Precision.
- The model has not been validated using real marketing campaign outcomes.
- The classification threshold should ultimately be selected based on actual business costs and objectives.

## Conclusion

The project demonstrates how Machine Learning can be applied to customer targeting in bank marketing.

The results show that addressing class imbalance can substantially improve the model's ability to identify potential subscribers.

The Balanced Logistic Regression model achieved a Recall of 0.83 for the `yes` class compared with 0.34 from the baseline model.

From a business perspective, the model can support marketing teams in prioritizing customers with higher subscription potential and improving marketing campaign targeting.

However, the model should be further validated using real campaign data and business-specific costs before being considered for production use.


## Tools & Technologies

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- SHAP
- Jupyter Notebook
