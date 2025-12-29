# Model Card: FICO HELOC Risk Classifier

## 🛠️ How to Reproduce Results

To ensure the results are consistent with the reported metrics, please follow these steps:

Environment Setup
Clone this repository and install the necessary dependencies:
```bash
git clone [https://github.com/YourUsername/YourRepoName.git](https://github.com/YourUsername/YourRepoName.git)
cd YourRepoName
pip install -r requirements.txt
```

## 1. Model Details
- **Developed by:** Ali-Abbass
- **Model Date:** December 2025
- **Model Type:** Logistic Regression (White-Box Baseline)
- **Framework:** Scikit-Learn
- **Performance Metric:** ROC AUC = 0.7909

## 2. Intended Use
- **Primary Use Case:** Predicting the probability of "Bad" credit performance (90+ days delinquent) for Home Equity Line of Credit (HELOC) applications.
- **Target Audience:** Credit Risk Managers and Regulatory Compliance Officers.
- **Decision Logic:** The model outputs a probability $P(\text{Bad})$. If $P > 0.5$, the applicant is flagged as high risk.


## 3. Data & Preprocessing
- **Source:** FICO HELOC Dataset (Anonymized).
- **Features:** 20 Numerical variables + 13 Binary Missingness Flags.
- **Handling Special Values:** Codes -7 (Condition Not Met), -8 (No Usable Trades), and -9 (No Record) were converted into binary flags to preserve the predictive power of "Missingness."
- **Feature Selection:** Pruned for Multicollinearity ($r > 0.85$). 
  - *Dropped:* `NumInqLast6m`, `NumTrades60Ever2DerogPubRec`, and `NumTotalTrades`.
  - 
## 4. Quantitative Analysis
The model was compared against a Challenger Random Forest. While the Random Forest achieved a slightly higher AUC (0.7944), the Logistic Regression (0.7909) was selected to meet the **Fair Credit Reporting Act (FCRA)** requirements for transparency.

| Metric | Training Set | Test Set |
| :--- | :--- | :--- |
| **ROC AUC** | 0.8012 | **0.7909** |
| **Accuracy** | 0.72 | 0.71 |


## 5. Interpretability (Reason Codes)
The model provides direct coefficients which can be used to generate "Adverse Action Notices."

### Top Risk Drivers:
1. **ExternalRiskEstimate:** Strongest predictor. Higher scores significantly reduce risk ($OR \approx 0.67$).
2. **NetFractionRevolvingBurden:** High utilization increases default risk ($OR \approx 1.40$).
3. **NumSatisfactoryTrades:** Longevity and quality of credit history reduce risk.


## 6. Ethical Considerations & Limitations
- **Limitations:** The model is a snapshot in time. It does not account for sudden macroeconomic shifts (e.g., inflation spikes).
- **Fairness:** No protected class features (race, gender, etc.) are included in the dataset, ensuring a "Blind" credit assessment process.
