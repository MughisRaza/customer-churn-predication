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

- Chosen model: XGBoost (tuned), because its CV AUC (0.8502 +/- 0.0117) was the highest of the three
  candidates (LR 0.8464 +/- 0.0129, RF 0.8464 +/- 0.0114). The choice was made from the CV table only,
  and the test set was used once afterwards. The margin is small: XGBoost leads by 0.0038, about
  one-third of a standard deviation, so it is a slight edge, not a clear win. LR and RF are tied.
- Single test AUC = 0.8483. CV mean +/- 2 std = [0.827, 0.874] (0.8502 -/+ 2 x 0.0117).
  Inside the interval? Yes. The test AUC is only 0.0019 below the CV mean, far less than one std,
  so the CV estimate was honest. The small drop is consistent with the winner's curse (the CV score
  was the best of many tuned settings) and ordinary split noise. At the 0.5 threshold the model has
  recall 0.521 and precision 0.659: it catches about half of the churners, and about two-thirds of
  the customers it flags actually churn.
- My Week 2 best model scored [your Week 2 number]. Tuning gained [test AUC 0.8483 minus your Week 2
  number]. [Explain it: if the gain is under about 0.01, that is within one CV std (about 0.012),
  so tuning gave little real improvement. The LR validation curve was flat from C = 1 upward, and
  grid, random search and the other settings all landed within about 0.001 of each other, which
  suggests this dataset has a performance ceiling around AUC 0.85 that no model family breaks.]
