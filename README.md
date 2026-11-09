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

Seeds min/max: 0.78 0.828
Grid time / Random time: 76 82
RF best params: {'max_depth': 15, 'max_features': np.float64(0.21273937997981013), 'min_samples_leaf': 15}
             model  cv_auc  cv_std
      LR (tuned C)  0.8464  0.0129
RF (random search)  0.8464  0.0114
   XGBoost (tuned)  0.8502  0.0117
Chosen k: 4
         customers  tenure  monthly  services  churn_rate
cluster                                                  
1             2157   18.38    80.41      3.28        0.43
3             1918    8.96    37.71      1.20        0.32
2             1938   59.83    92.09      5.06        0.14
0             1030   53.61    30.96      1.48        0.05
PCA 90%: 15 of 30
