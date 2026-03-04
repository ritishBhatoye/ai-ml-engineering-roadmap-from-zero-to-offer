<![CDATA[# Project 2: Supervised ML Pipeline

## 🎯 Objective
Build a complete, production-quality ML pipeline: preprocessing → feature engineering → model selection → hyperparameter tuning → evaluation. Demonstrate engineering rigor, not just model accuracy.

## 📊 Suggested Datasets
- [Ames Housing](https://www.kaggle.com/c/house-prices-advanced-regression-techniques) — regression
- [Telco Customer Churn](https://www.kaggle.com/blastchar/telco-customer-churn) — classification
- [Bank Marketing](https://archive.ics.uci.edu/ml/datasets/bank+marketing) — classification

## 📋 Deliverables Checklist

- [ ] **Data preprocessing** — missing values, encoding, scaling (use sklearn Pipeline)
- [ ] **Feature engineering** — 5+ engineered features with reasoning
- [ ] **Baseline model** — logistic regression or simple decision tree
- [ ] **Multi-model comparison** — compare 3+ models (Random Forest, XGBoost, etc.)
- [ ] **Hyperparameter tuning** — RandomizedSearchCV with cross-validation
- [ ] **Evaluation report** — metrics table, confusion matrix, ROC curve, learning curves
- [ ] **Modular code** — `src/` directory with separate modules
- [ ] **Config file** — YAML config for all hyperparameters
- [ ] **README** — with results table, key decisions, and how to run

## 🏗 Suggested Structure

```
02-supervised-pipeline/
├── config/
│   └── config.yaml
├── src/
│   ├── data.py
│   ├── features.py
│   ├── model.py
│   └── evaluate.py
├── notebooks/
│   └── exploration.ipynb
├── train.py
├── requirements.txt
└── README.md
```

## ⏱ Estimated Time: 15–20 hours
]]>
