# Project 2: Supervised ML Pipeline

## Objective

Build a complete, production-quality ML pipeline: preprocessing → feature engineering → model selection → hyperparameter tuning → evaluation.

**Why this matters:** This is what interviewers expect you to build in 45 minutes during a coding round. They want to see engineering rigor, not just model accuracy.

---

## Suggested Datasets

| Dataset | Type | Source |
|---------|------|--------|
| Ames Housing | Regression | [Kaggle](https://www.kaggle.com/c/house-prices-advanced-regression-techniques) |
| Telco Customer Churn | Classification | [Kaggle](https://www.kaggle.com/blastchar/telco-customer-churn) |
| Bank Marketing | Classification | [UCI](https://archive.ics.uci.edu/ml/datasets/bank+marketing) |
| Porto Seguro | Classification | [Kaggle](https://www.kaggle.com/c/porto-seguro-safe-driver-prediction) |

---

## Deliverables Checklist

### Preprocessing
- [ ] Missing value handling with justification
- [ ] Categorical encoding (one-hot, target, ordinal as appropriate)
- [ ] Feature scaling (standardization, normalization)
- [ ] Use sklearn Pipeline for reproducibility

### Feature Engineering
- [ ] 5+ engineered features with clear reasoning
- [ ] Document feature importance analysis

### Modeling
- [ ] Baseline model (Logistic Regression or Decision Tree)
- [ ] Multi-model comparison (3+ models: RF, XGBoost, etc.)
- [ ] Hyperparameter tuning (RandomizedSearchCV with cross-validation)
- [ ] Proper train/validation/test split

### Evaluation
- [ ] Metrics table comparing all models
- [ ] Confusion matrix visualization
- [ ] ROC curve (for classification) or residual plots (for regression)
- [ ] Learning curves to diagnose overfitting/underfitting

### Code Quality
- [ ] Modular code structure (`src/` directory)
- [ ] YAML config file for hyperparameters
- [ ] Requirements.txt with versions
- [ ] README with results table and key decisions

---

## Assessment Criteria

| Criterion | Weight | What Interviewers Look For |
|-----------|--------|---------------------------|
| Pipeline Design | 25% | Clean sklearn Pipeline, proper preprocessing |
| Feature Engineering | 20% | Thoughtful features with business reasoning |
| Model Selection | 20% | Proper comparison of multiple algorithms |
| Evaluation | 20% | Rigorous metrics, learning curves, no data leakage |
| Code Quality | 15% | Modular, reproducible, documented |

---

## Suggested Structure

```
02-supervised-pipeline/
├── config/
│   └── config.yaml             # All hyperparameters
├── src/
│   ├── __init__.py
│   ├── data.py                # Data loading
│   ├── features.py            # Feature engineering
│   ├── model.py               # Model training
│   └── evaluate.py            # Evaluation
├── notebooks/
│   └── exploration.ipynb      # EDA and experimentation
├── tests/
│   └── test_pipeline.py       # Basic tests
├── train.py                   # Main training script
├── evaluate.py                # Evaluation script
├── requirements.txt
└── README.md
```

---

## Starter Code

```yaml
# config/config.yaml
data:
  path: "data/raw/train.csv"
  target: "target_column"
  test_size: 0.2

preprocessing:
  numeric_features: ["feature1", "feature2"]
  categorical_features: ["cat1", "cat2"]
  missing_strategy: "median"

model:
  name: "xgboost"
  params:
    n_estimators: 300
    max_depth: 6
    learning_rate: 0.1
    subsample: 0.8

tuning:
  n_iter: 50
  cv: 5
  scoring: "roc_auc"
```

```python
# src/model.py
import yaml
from pathlib import Path
from sklearn.ensemble import RandomForestClassifier, GradientBoostingClassifier
from sklearn.linear_model import LogisticRegression
import xgboost as xgb

def get_model(config: dict):
    """Factory function to create model from config."""
    model_name = config['model']['name']
    params = config['model'].get('params', {})
    
    models = {
        'logistic': LogisticRegression(**params),
        'random_forest': RandomForestClassifier(**params),
        'xgboost': xgb.XGBClassifier(**params),
        'gradient_boosting': GradientBoostingClassifier(**params),
    }
    
    return models.get(model_name, LogisticRegression())
```

```python
# train.py
import yaml
from src.data import load_data
from src.features import create_pipeline
from src.model import get_model
from sklearn.model_selection import RandomizedSearchCV

def main():
    # Load config
    with open('config/config.yaml') as f:
        config = yaml.safe_load(f)
    
    # Load data
    df = load_data(config['data']['path'])
    
    # Create pipeline
    pipeline = create_pipeline(config)
    
    # Split
    X = df.drop(columns=[config['data']['target']])
    y = df[config['data']['target']]
    
    # Train with hyperparameter tuning
    model = get_model(config)
    search = RandomizedSearchCV(
        pipeline, 
        config['tuning'],
        n_iter=config['tuning']['n_iter'],
        cv=config['tuning']['cv'],
        scoring=config['tuning']['scoring'],
        random_state=42
    )
    search.fit(X, y)
    
    print(f"Best score: {search.best_score_}")
    print(f"Best params: {search.best_params_}")

if __name__ == "__main__":
    main()
```

---

## Common Interview Questions for This Project

1. Why did you choose these preprocessing steps?
2. How did you handle class imbalance?
3. What feature engineering improved performance?
4. Explain your hyperparameter search strategy
5. How would you deploy this model?

---

## Estimated Time: 15–20 hours
