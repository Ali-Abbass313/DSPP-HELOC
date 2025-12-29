# 📋 Model Card: FICO HELOC Risk Classifier

> **Version:** 1.0 (Baseline Winner)  
> **Last Updated:** December 2025  
> **Status:** ![Stable](https://img.shields.io/badge/Status-Stable-green)

---

## 1. Project Overview
This model was developed as part of a **Professional Practice** module to predict credit risk using the FICO HELOC dataset. The goal was to build a transparent, high-performing classifier suitable for a regulated financial environment.

## 2. Model Architecture
- **Type:** Logistic Regression (Standardized)
- **Framework:** `scikit-learn` Pipeline
- **Key Features:** 58 variables (including 35 indicator flags for missing values)

## 3. Performance Metrics
| Metric | Result | Benchmark |
| :--- | :--- | :--- |
| **ROC-AUC** | **0.7751** | > 0.70 |
| **CV Stability (Std Dev)** | **0.0361** | < 0.05 |

## 4. Explainability (SHAP)
To meet **GDPR "Right to Explanation"** standards, this model integrates SHAP values. 
- **Primary Risk Factor:** `ExternalRiskEstimate` (Negative correlation)
- **Primary Burden Factor:** `NetFractionRevolvingBurden` (Positive correlation)

## 5. How to Reproduce
To run this model, ensure you have the following environment:
```python
pip install numpy==1.26.4 scipy==1.11.4 scikit-learn==1.4.0 shap==0.44.1
