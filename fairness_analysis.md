# Model Fairness, Bias, and Explainability Analysis Report

## Overview

This project analyzes a Random Forest Classifier for customer churn prediction using the Telco Customer Churn dataset.

- **Dataset:** `customer_churn_data.csv`
- **Total records:** 5,880
- **Target variable:** `Churn` (Yes/No)
- **Sensitive attributes:** Gender and SeniorCitizen
- **Baseline model:** RandomForestClassifier
- **Mitigation technique:** SMOTE (Synthetic Minority Over-sampling Technique)

The project evaluates model performance, feature importance, explainability, and fairness across demographic groups.

## 1. Feature Importance

Feature importance was calculated using the Random Forest model's `feature_importances_` attribute.

The three most important features in the generated chart were:

1. MonthlyCharges
2. TotalCharges
3. tenure

These features contributed most to the model's prediction process according to the Random Forest feature importance scores.

Feature importance indicates how the model uses features; it does not establish that these features cause customer churn.

## 2. Global Explainability: SHAP

SHAP (SHapley Additive exPlanations) was used to understand how individual features influence the model's predictions.

The SHAP summary plot showed that:

- TotalCharges
- tenure
- MonthlyCharges

were among the most influential features.

The summary plot displays the direction and magnitude of feature contributions across the evaluated customers.

## 3. Local Explainability: LIME

LIME (Local Interpretable Model-agnostic Explanations) was used to explain an individual customer prediction.

For the displayed test customer, the model predicted:

- No Churn: 0.47
- Churn: 0.53

The model therefore slightly favoured the Churn class for this customer.

LIME displayed the feature contributions associated with this individual prediction.

## 4. Fairness and Bias Detection

Fairness was evaluated using two sensitive attributes:

- `gender_Male`: 0 represents Female and 1 represents Male.
- `SeniorCitizen`: 0 represents Non-Senior Citizen and 1 represents Senior Citizen.

The following metrics were calculated:

- **Accuracy:** Percentage of correct predictions.
- **FPR:** False Positive Rate.
- **TPR:** True Positive Rate.
- **Prediction Rate:** Percentage of customers predicted to churn.

### Before Mitigation (Baseline Model)

| Group | Accuracy | FPR | TPR | Prediction Rate |
|---|---:|---:|---:|---:|
| Female | 0.4930 | 0.4698 | 0.4567 | 0.4632 |
| Male | 0.4917 | 0.4794 | 0.4605 | 0.4703 |
| Senior Citizen | 0.4899 | 0.4872 | 0.4645 | 0.4764 |
| Non-Senior Citizen | 0.4725 | 0.4965 | 0.4429 | 0.4691 |

The baseline model showed differences in some metrics between demographic groups.

## 5. Bias Mitigation Using SMOTE

SMOTE was applied to the training data to address class imbalance.

A separate Random Forest model (`fair_model`) was trained using the resampled training dataset. The original baseline model was retained for comparison.

### After Mitigation (SMOTE Model)

| Group | Accuracy | FPR | TPR | Prediction Rate |
|---|---:|---:|---:|---:|
| Female | 0.4719 | 0.4804 | 0.4256 | 0.4526 |
| Male | 0.5000 | 0.4762 | 0.4742 | 0.4752 |
| Senior Citizen | 0.5000 | 0.4615 | 0.4574 | 0.4596 |
| Non-Senior Citizen | 0.4725 | 0.4965 | 0.4429 | 0.4691 |

### Model Performance Comparison

| Metric | Baseline | After SMOTE |
|---|---:|---:|
| Accuracy | 49.23% | 48.64% |

The baseline model achieved slightly higher accuracy than the SMOTE-trained model.

### Fairness Comparison

SMOTE produced mixed results:

- The gender FPR difference decreased from approximately 0.96 to 0.42 percentage points.
- The gender accuracy difference increased from approximately 0.12 to 2.81 percentage points.
- The SeniorCitizen FPR difference increased from approximately 0.93 to 3.49 percentage points.
- The SeniorCitizen TPR difference decreased from approximately 2.16 to 1.45 percentage points.

Therefore, SMOTE did not consistently improve fairness across all demographic groups.

**Important:** SMOTE was used to balance target classes in the training data. It was not a direct demographic fairness mitigation technique.

## 6. Mitigation Recommendations

1. **SMOTE:** Evaluate oversampling techniques to address class imbalance.
2. **Reweighting:** Explore sample weighting to improve model learning.
3. **Fairness-aware methods:** Evaluate techniques designed to reduce demographic disparities.
4. **Threshold adjustment:** Study how prediction thresholds affect group-level metrics.
5. **Continuous monitoring:** Regularly evaluate FPR, TPR, accuracy, and prediction rates across demographic groups.
6. **Explainability audits:** Use SHAP and LIME to understand model predictions.

## 7. Conclusion

This project implemented a Random Forest Classifier for customer churn prediction and evaluated its performance using classification metrics.

Feature Importance, SHAP, and LIME were used to understand global and individual model behaviour.

Fairness was evaluated across gender and SeniorCitizen groups using accuracy, FPR, TPR, and prediction rate.

The baseline model achieved approximately 49.23% accuracy, while the SMOTE-trained model achieved approximately 48.64%.

The fairness comparison showed mixed results. Some group-level metric differences decreased, while others increased.

The experiment demonstrates that balancing target classes does not automatically eliminate demographic disparities. Both predictive performance and fairness must be evaluated when developing machine learning models.
:::
