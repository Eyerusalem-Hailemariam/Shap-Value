Customer Churn Analysis & Explainability Report
1. Objective
The goal was to predict customer churn and understand why certain customers are likely to churn using a Random Forest classifier with SHAP explainability. Key objectives included:
Identifying features driving churn predictions.


Understanding individual customer risk factors.


Exploring feature interactions and overall feature importance.


2. Data Overview & Preparation
Dataset: 3,150 customers with 13 features and a Churn target column.


Class Distribution: 84% non-churn, 16% churn (imbalanced).


Preprocessing:


One-hot encoding for categorical features.


Train/test split: 70% train (2,205 samples), 30% test (945 samples).


SMOTE applied to balance the training set: 1,845 samples per class.


3. Model Training & Performance
Customer Churn Analysis & Explainability Report

Executive summary
This analysis uses a Random Forest classifier together with SHAP explainability to predict customer churn and identify the features driving those predictions. The model achieves strong overall performance and SHAP provides both global and per-customer insights that support targeted retention strategies.

1. Objective
- Predict which customers are likely to churn.
- Explain model predictions at the global and individual level using SHAP so business teams can act on the results.

2. Data overview & preparation
- Dataset: 3,150 customers, 13 features, and a binary `Churn` target.
- Class distribution: ~84% non-churn, ~16% churn (class imbalance).
- Preprocessing steps:
	- One-hot encoding for categorical features.
	- Train/test split: 70% train (2,205 samples), 30% test (945 samples).
	- SMOTE applied to the training set to address imbalance (resulting in ~1,845 samples per class in the training set).

3. Model training & performance
- Model: Random Forest classifier (200 trees, random_state=1).
- Test set performance (selected metrics):
	- Accuracy: 95%
	- Class 0 (No churn): Precision = 0.98, Recall = 0.96, F1 = 0.97
	- Class 1 (Churn): Precision = 0.79, Recall = 0.90, F1 = 0.84

Interpretation: The model achieves high overall accuracy with especially strong recall for the churn class, meaning it successfully identifies most customers who will churn (useful for prioritizing retention efforts). Precision for churn is lower than for the non-churn class, so some false positives are expected.

4. SHAP explainability results
4.1 Global feature influence
- SHAP summary plots show the direction and strength of each feature's impact on predictions.
- Top features by mean absolute SHAP value include: Call Failure, Subscription Length, Charge Amount, Seconds of Use, and Customer Value.

4.2 Dependence and interaction effects
- Dependence plots reveal nonlinear relationships (for example, low Customer Value is associated with a sharp increase in churn probability).
- SHAP interaction values highlight feature pairs with strong joint effects, which can inform combined interventions.

4.3 Individual explanations
- Waterfall/force plots identify which features push a given customer's prediction toward churn or retention. These plots are actionable for designing personalized retention offers.

4.4 Decision plots
- Decision plots show cumulative contributions of features for specific customers, useful for explaining model decisions to stakeholders.

5. Comparison with other importance measures
- Compared to MDI (feature importance from Random Forest) and permutation importance, SHAP provides both magnitude and direction for each feature's effect. The top features are broadly consistent across methods, increasing confidence in the results.

6. Business recommendations
- Prioritize retention campaigns for customers flagged as high-risk (high churn SHAP scores), especially when key drivers like recent call failures or low customer value are present.
- Investigate pricing or billing issues for customers with high `Charge Amount` contributions to churn.
- Use feature interaction insights to tailor offers (for example, longer-term discounts for customers with short subscription length and low usage).

7. Reproducibility
- The analysis is implemented in the notebook `Untitled6.ipynb` in this repository.
- To reproduce the environment quickly, use a virtualenv and install the core packages:

```bash
python -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install jupyter numpy pandas scikit-learn shap matplotlib seaborn imbalanced-learn
```

Open the notebook and run the cells to reproduce preprocessing, model training, and SHAP visualizations.

8. Limitations
- The dataset is imbalanced; SMOTE was used to mitigate this but synthetic samples can affect model behavior.
- Results depend on the chosen model and hyperparameters; further tuning or alternative models (e.g., XGBoost) may improve performance.
- External validation on a holdout period or a different dataset is recommended before deploying actions.

9. Contact
For questions or requests (e.g., a pinned `requirements.txt`, model code extraction, or a renamed notebook), contact the analysis owner or update the repository and I can generate the requested artifact.


Helps refine business strategies by understanding how features jointly affect churn risk.




