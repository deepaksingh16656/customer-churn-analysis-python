# Telecom Customer Churn Analysis

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/deepaksingh16656/telecom-churn-analysis/blob/main/Customer_Churn_Analysis.ipynb)

An end-to-end churn analysis on a telecom customer dataset: data cleaning, exploratory analysis answering business questions, a machine learning model, explainability with SHAP, and retention recommendations.

> **Business question:** Why are customers leaving, who is most at risk, and what should the company do about it?

---

## Dataset

- 100,000 customers, 100 columns (usage, billing, handset, service quality, customer care, tenure, demographics)
- Target: `churn` (1 = churned, 0 = retained)
- Source: **[add the dataset link and license here]**
- **The data is not included in this repository.** Download it from the source above and place `Telecom_customer churn.csv` in the same folder as the notebook.

> The sample is balanced (about 49.6% churn). Real carriers usually see much lower churn, so the model should be recalibrated before use on real company data.

---

## What I did

1. **Data cleaning:** median imputation for numeric columns, an explicit "Unknown" category for missing categoricals, `U` standardized to "Unknown", negative `rev_Mean` and `eqpdays` values floored at 0, and 1st/99th percentile capping on heavy-tailed usage columns. No rows were dropped.
2. **Exploratory analysis:** churn by customer lifecycle, handset age and price, usage trends, revenue, service quality, customer care contact, demographics, geography and credit class. Chi-square tests with Cramér's V, and Mann-Whitney tests with effect sizes.
3. **Modeling:** engineered features, a leakage-safe stratified 80/20 split with target encoding fitted on training data only, Logistic Regression vs Random Forest vs LightGBM, 5-fold cross-validation, and hyperparameter tuning of LightGBM.
4. **Explainability and action:** SHAP feature importance, customer risk tiers, and a retention campaign simulation.

---

## Key findings

| Finding | Result |
|---|---|
| Handset age is the clearest signal | Churn rises from **39.9%** (0-90 days) to **57.9%** (731+ days), with a jump past 365 days (47.0% to 53.7%) |
| Handset price | Handsets under $50 churn at **57.5%**, over $200 at **36.0%** |
| Falling usage | A decline of more than 100 minutes: **53.6%** churn, against **46.2%** for growing usage |
| Customer care contact | 0 calls: **51.8%** churn, 6+ calls: **44.2%** (an association, likely linked to engagement and usage) |
| Tenure | The 0-6 month band has the lowest churn (**38.4%**), and 13-24 months the highest (**51.8%**) |
| Geography | Highest: Northwest/Rocky Mountain (**56.9%**). Lowest: Midwest (**45.9%**) |
| Demographics | Weak. Every Cramér's V is below 0.10, which is negligible |

All findings are **associations, not proof of cause.** With 100,000 rows, small effects can show tiny p-values, so effect sizes matter more than significance.

---



---

## Recommendations

1. Proactive upgrade offers for customers whose handsets are approaching one year old
2. An onboarding and engagement program for the first months
3. Win-back outreach for customers with sharply declining usage
4. Proactive care outreach to customers who never contact support
5. Entry-level handset and leasing options for low-price-handset customers
6. Network quality monitoring and bill-shock alerts for heavy overage or roaming users

---

## Limitations

- Balanced churn sample, unlike real-world churn rates
- Heavy missing data in demographic fields (some columns are over 90% unknown)
- Associations, not causal effects
- Undocumented codes in some columns (for example `hnd_webcap`)
- Unknown data collection period, and no contract information
- Imputation and capping were fitted on the full dataset before the train/test split (a minor leakage risk)
- Demographic fields such as ethnicity, marital status and income are sensitive and must not be used for targeting or pricing decisions

---

## How to run

```bash
git clone https://github.com/deepaksingh16656/telecom-churn-analysis.git
cd telecom-churn-analysis
pip install -r requirements.txt
# place "Telecom_customer churn.csv" in this folder, then:
jupyter notebook Customer_Churn_Analysis.ipynb
```

Or click the **Open in Colab** badge above and upload the dataset to the session.

---

## Tools

Python, pandas, NumPy, Matplotlib, Seaborn, SciPy, scikit-learn, LightGBM, SHAP

## License

MIT. See `LICENSE`. The dataset is subject to its own license.
