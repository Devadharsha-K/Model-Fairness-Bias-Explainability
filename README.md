# Model Fairness, Bias, and Explainability Analysis

## Overview

This project analyzes a Random Forest Classifier for customer churn prediction using the Telco Customer Churn dataset.

The project focuses on model performance, fairness evaluation, bias detection, and explainability using SHAP and LIME.

## Dataset

- **File:** `customer_churn_data.csv`
- **Records:** 5,880
- **Target:** Churn (Yes/No)
- **Sensitive attributes:** Gender and SeniorCitizen

## Environment Setup

1. Ensure Python 3.8 or later is installed.
2. Install the required dependencies:

```bash
pip install -r requirements.txt
```

Required libraries include pandas, numpy, scikit-learn, matplotlib, shap, lime, and imbalanced-learn.

## Running the Analysis

1. Open `Task3_Cleaned_Organized.ipynb` in Jupyter Notebook or VS Code.
2. Select the appropriate Python environment.
3. Run all notebook cells sequentially.

The notebook includes:

- Data loading and exploratory data analysis.
- Data preprocessing and one-hot encoding.
- Random Forest model training and evaluation.
- Feature importance visualization.
- SHAP global explainability.
- LIME local explainability.
- Fairness evaluation using Accuracy, FPR, TPR, and Prediction Rate.
- SMOTE-based resampling and model comparison.
- Before-and-after fairness analysis.

## Key Outputs

### Feature Importance
Identifies the features that contribute most to the Random Forest model's predictions.

### SHAP
Provides global explanations of feature contributions to model predictions.

### LIME
Explains individual customer predictions.

### Fairness Analysis
Evaluates model outcomes across:
- Gender (gender_Male: 0 = Female, 1 = Male)
- SeniorCitizen (0 = Non-Senior Citizen, 1 = Senior Citizen)

### SMOTE Comparison
Compares baseline and SMOTE-trained models.

The baseline model achieved approximately 49.23% accuracy, while the SMOTE-trained model achieved approximately 48.64%.

SMOTE produced mixed fairness results and did not consistently reduce demographic disparities.

## Project Files

- `Task3_Cleaned_Organized.ipynb` – Main analysis notebook.
- `customer_churn_data.csv` – Dataset.
- `requirements.txt` – Required Python libraries.
- `fairness_analysis.md` – Detailed project report.
- `screenshot 1.png` and `Screenshot 2.png` – Existing project screenshots.

## Conclusion

This project demonstrates customer churn prediction using Random Forest, model explainability using SHAP and LIME, and fairness evaluation across demographic groups.

It also examines the effect of SMOTE on model performance and fairness, highlighting the importance of evaluating both predictive accuracy and demographic disparities.
:::