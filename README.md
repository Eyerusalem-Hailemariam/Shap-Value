# Customer Churn Analysis & Explainability Report

## 1. Objective
The goal was to predict customer churn and understand why certain customers are likely to churn using a Random Forest classifier with SHAP explainability.

Key objectives included:
- Identifying features driving churn predictions.
- Understanding individual customer risk factors.
- Exploring feature interactions and overall feature importance.

## 2. Data Overview & Preparation
- **Dataset:** 3,150 customers with 13 features and a `Churn` target column.
- **Class Distribution:** 
  - 84% non-churn  
  - 16% churn (imbalanced)
- **Preprocessing:**
  - One-hot encoding for categorical features.
  - Train/test split: 70% train (2,205 samples), 30% test (945 samples).
  - SMOTE applied to balance the training set: 1,845 samples per class.

## 3. Model Training & Performance
- **Model:** Random Forest (200 trees, `random_state=1`)
- **Test Set Metrics:**
  - **Accuracy:** 95%
  - **Class 0 (No churn):** Precision 0.98, Recall 0.96, F1-score 0.97
  - **Class 1 (Churn):** Precision 0.79, Recall 0.90, F1-score 0.84

**Insight:** High recall for churn indicates the model effectively identifies at-risk customers.

## 4. SHAP Explainability

### 4.1 Global Feature Influence
- **Summary Plots (Class-specific):**
  - Class 0 (No Churn): Negative SHAP values indicate features supporting retention.
  - Class 1 (Churn): Positive SHAP values indicate features driving churn risk.
- **Top Features (by mean absolute SHAP values):**
  - Call Failure
  - Subscription Length
  - Charge Amount
  - Seconds of Use
  - Customer Value
- **Interpretation:** Features with higher |SHAP values| have the strongest impact on predictions regardless of direction.

### 4.2 Dependence Plots
- Continuous features show nonlinear effects on churn probability.
- **Example:** Low Customer Value sharply increases churn risk.
- Feature interactions provide insights for targeted retention strategies.

### 4.3 Individual Predictions
- Most likely to churn: Waterfall and force plots highlight which features push predictions toward churn.
- Least likely to churn: Plots show features that reduce churn probability.
- **Business Insight:** Enables personalized retention actions for high-risk customers.

### 4.4 Decision Plots
- Show cumulative feature impact on predicted probability for each class.
- Top 3 high-risk customers: Cumulative feature contributions clearly drive churn prediction.
- Top 3 low-risk customers: Features push predictions toward retention.

### 4.5 Feature Interactions
- SHAP interaction values identify pairs of features with strong combined influence.
- Helps refine business strategies by understanding how features jointly affect churn risk.

## 5. Comparison of Feature Importance
- Compared **MDI**, **Permutation**, and **SHAP**:
  - SHAP highlights both magnitude and direction of feature influence.
  - Top features are consistent across methods, validating the model’s focus.

## 6. Key Takeaways
- **High-risk factors:** Call failures, short subscription length, high charges, low usage or customer value.
- **Retention factors:** Long subscription, stable usage, and high customer value.
- **SHAP interpretability:** Provides global and individual insights for actionable decisions.
- **Decision plots and interactions:** Useful for identifying cumulative and synergistic effects on churn.
- **Business insight:** Focus retention campaigns on high-risk customers and key influencing features.


