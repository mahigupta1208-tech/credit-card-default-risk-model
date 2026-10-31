# credit-card-default-risk-model
PD model, validation and cut-off analysis on credit card data
# Credit Card Default Risk Model & Validation

## Problem
A card issuer loses money when customers default. This project builds a model that predicts each customer's Probability of Default (PD), validates it the way a bank's model-risk team would, and shows how an approval cut-off trades growth against losses.

## Data
UCI "Default of Credit Card Clients" (Kaggle: `UCI_Credit_Card.csv`): 30,000 accounts, 22.1% default rate. Not included in this repository; download it and place it next to the notebook.

## Method
1. Data check: no missing values; undocumented codes in EDUCATION and MARRIAGE (about 1% of accounts), not used in the model
2. Features: credit utilization, payment ratio, maximum payment delay
3. Logistic regression (explainable, standard for bank scorecards)
4. Validation: AUC, Gini, KS, and predicted vs actual default rate by decile
5. Improvement: calibration showed under-prediction for the safest customers. The cause was PAY_0 (repayment status) being treated as numeric, so I encoded it as a category.
6. Cut-off table: approval rate, bad rate and profit at different cut-offs (first model, placeholder profit values)

## Results

| Metric | First model | Final model |
|---|---|---|
| AUC | 0.724 | 0.745 |
| Gini | 44.7% | 49.0% |
| KS | 38.5% | 38.9% |
| Safest decile, predicted vs actual | 4.4% vs 13.7% | 7.3% vs 7.3% |

In the final model, predicted and actual default rates are within about 2.5 percentage points in every decile.

## Limitations and future work
- One country, one time period, no macroeconomic variables, no reject inference
- Profit values are assumptions, not bank data
- Not done: PSI stability testing, a challenger model (decision tree), and monitoring over time (the dataset has no dates)

## How to run
Open the notebook in Google Colab, upload `UCI_Credit_Card.csv`, and choose Runtime > Run all.

## Tools
Python, pandas, NumPy, scikit-learn
