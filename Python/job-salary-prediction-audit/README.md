# Job Salary Prediction Audit

## Overview
This project audits an automated job salary prediction system trained on UK job advertisement data (Adzuna/Kaggle). We evaluate the model’s **accuracy**, **fairness across job categories**, and **stability/generalization** to understand how well it performs and where it may underperform for specific groups.

## Why this matters
Many job ads do not disclose salary. Salary prediction can improve transparency for job seekers—but if performance varies across categories, the system may create unequal outcomes or misleading estimates for certain job groups.

## Data
Source: Adzuna dataset from a Kaggle competition.  
Inputs include:
- **Title**, **FullDescription** (text)
- **LocationRaw**, **LocationNormalized**
- **ContractType** (full-time/part-time), **ContractTime** (permanent/contract)
- **Company**, **Category**, **SourceName**
Target:
- **SalaryNormalized** (annual salary)

Notes: Some fields contain substantial missingness (e.g., ContractType).

## Methods
### Preprocessing
- Created missing-value indicator features for selected columns
- Encoded categorical variables into numeric codes
- Split data into train/test sets

### Modeling
- Trained a **RandomForestRegressor** to predict **SalaryNormalized**
- Evaluated performance using **MAE**, **RMSE**, and **R²**
- Tuned hyperparameters using **RandomizedSearchCV** with **5-fold cross-validation**
- Reviewed **feature importance** for model validation

### Fairness evaluation (category-level)
To assess fairness-related behavior across job categories, we binarized salary outcomes using the **overall mean SalaryNormalized** as a threshold and computed:
- **Precision, Recall, F1**
- **TPR (True Positive Rate)** and **FPR (False Positive Rate)**

### Stability
- Compared test-set MAE to cross-validated MAE
- Examined fold-to-fold variation to assess consistency

## Key Results (high-level)
- Performance was strong for many categories, with high R² values overall.
- Some categories showed higher error (e.g., **Domestic Help & Cleaning Jobs**, **Social Work Jobs**), indicating weaker predictive performance.
- Fairness metrics were generally consistent across categories, but **Domestic Help & Cleaning Jobs** showed low precision (high false positives) despite high recall.
- Cross-validation MAE was slightly higher than the original MAE, suggesting the original split may be optimistic, but fold results were relatively close—indicating stable generalization.

## Limitations
- Random forests are accurate but less interpretable for end users.
- SHAP/LIME interpretability was attempted but was not feasible due to compute constraints.
- Missingness and unobserved features (e.g., seniority, education, benefits) may reduce accuracy for certain categories.

## Tools
Python, Pandas, NumPy, scikit-learn, Matplotlib

## Reference
Original ADS notebook (Jillani Soft Tech):  
https://www.kaggle.com/code/jillanisofttech/job-salary-prediction-by-jst/notebook

