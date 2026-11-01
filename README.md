# Customer Churn Prediction

## Week 1: Exploratory Data Analysis

### Dataset
- Source: Telco Customer Churn (Kaggle)
- Size: 7,043 customers, 21 features
- Target: Predict customer churn (Yes/No)

### Key Findings
- Overall churn rate is about 26.5% (roughly 1 in 4 customers left).
- Month-to-month contracts churn at 42.7%, vs 11.3% for one-year and 2.8% for two-year contracts.
- The first 6 months are the riskiest: 52.9% of customers with 0-6 months of tenure churn, vs only 9.5% for customers with 49+ months.
- Fiber optic customers churn at 41.9%, more than double DSL customers (19.0%).
- Electronic check users churn at 45.3%, about 3x more than automatic payment users (15-17%).
- Customers paying over $70/month churn at 35.4% vs 17.4% for those paying less.

### Setup
Open the Kaggle notebook or run locally:

pip install pandas numpy matplotlib seaborn

Week 2: Building ML Models
- Baseline (always "stay"): accuracy 0.735
- Best model: Logistic Regression, AUC 0.842, recall 0.754 at threshold 0.3
- Top churn drivers (permutation importance): tenure, TotalCharges, Contract_Two year
- Threshold chosen: 0.3, because a missed churner costs PKR 6,000 vs PKR 1,000 for an unneeded offer
- Engineered features: n_services, is_new, charge_per_mo, price_jump; effect on AUC: 0.842 -> 0.842
- Biggest lesson: Accuracy hides missed churners; the threshold is a business decision.

add Codeadd Markdown
