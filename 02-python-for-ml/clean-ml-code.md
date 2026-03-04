<![CDATA[# Writing Clean ML Code

> **Interview weight:** ⭐⭐⭐ — Evaluated during live coding and take-home assignments.  
> **Time to study:** 4–5 hours.  
> **Goal:** Write ML code that is readable, modular, reproducible, and production-ready.

---

## Why This Matters

Interviewers see two types of candidates:

1. **Notebook warrior:** All code in one giant Jupyter cell. Global variables everywhere. No functions. Copy-pasted from StackOverflow. 
2. **ML engineer:** Modular scripts. Config files. Reproducible pipelines. Clean abstractions.

Be candidate #2. It's a massive differentiator.

---

## The Production ML Project Structure

```
ml-project/
├── config/
│   └── config.yaml          # All hyperparameters and paths
├── src/
│   ├── __init__.py
│   ├── data.py              # Data loading and preprocessing
│   ├── features.py          # Feature engineering pipeline
│   ├── model.py             # Model definition and training
│   ├── evaluate.py          # Evaluation metrics and reporting
│   └── predict.py           # Inference logic
├── notebooks/
│   └── eda.ipynb            # Exploratory analysis (ONLY for exploration)
├── tests/
│   ├── test_data.py
│   └── test_model.py
├── train.py                 # Main training entry point
├── requirements.txt         # Pinned dependencies
├── Dockerfile               # For deployment
└── README.md
```

---

## Rule 1: Config, Don't Hardcode

```yaml
# config/config.yaml
data:
  train_path: "data/train.csv"
  test_path: "data/test.csv"
  target_column: "churn"

model:
  type: "xgboost"
  params:
    n_estimators: 200
    max_depth: 6
    learning_rate: 0.1
    
training:
  test_size: 0.2
  random_state: 42
  cv_folds: 5
```

```python
# train.py
import yaml

with open("config/config.yaml") as f:
    config = yaml.safe_load(f)

# Now use config["model"]["params"]["n_estimators"] instead of hardcoded 200
```

## Rule 2: Functions, Not Scripts

```python
# BAD — one long script
df = pd.read_csv("data.csv")
df = df.dropna()
df["age_bin"] = pd.cut(df["age"], bins=5)
# ... 200 lines of spaghetti

# GOOD — modular functions
def load_data(path: str) -> pd.DataFrame:
    """Load and validate raw data."""
    df = pd.read_csv(path)
    assert "target" in df.columns, "Target column missing"
    return df

def preprocess(df: pd.DataFrame) -> pd.DataFrame:
    """Handle missing values and create features."""
    df = df.copy()
    df["age"].fillna(df["age"].median(), inplace=True)
    df["age_bin"] = pd.cut(df["age"], bins=5, labels=False)
    return df
```

## Rule 3: Type Hints

```python
from typing import Tuple
import numpy as np
import pandas as pd
from sklearn.base import BaseEstimator

def train_model(
    X_train: np.ndarray,
    y_train: np.ndarray,
    model: BaseEstimator,
    params: dict,
) -> BaseEstimator:
    """Train a model with given parameters."""
    model.set_params(**params)
    model.fit(X_train, y_train)
    return model

def split_data(
    df: pd.DataFrame,
    target_col: str,
    test_size: float = 0.2,
) -> Tuple[np.ndarray, np.ndarray, np.ndarray, np.ndarray]:
    """Split DataFrame into train/test arrays."""
    from sklearn.model_selection import train_test_split
    X = df.drop(columns=[target_col]).values
    y = df[target_col].values
    return train_test_split(X, y, test_size=test_size, random_state=42)
```

## Rule 4: Sklearn Pipelines (Not Manual Preprocessing)

```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer
from sklearn.ensemble import RandomForestClassifier

numeric_features = ["age", "income", "tenure"]
categorical_features = ["city", "plan_type"]

numeric_pipeline = Pipeline([
    ("imputer", SimpleImputer(strategy="median")),
    ("scaler", StandardScaler()),
])

categorical_pipeline = Pipeline([
    ("imputer", SimpleImputer(strategy="most_frequent")),
    ("encoder", OneHotEncoder(handle_unknown="ignore")),
])

preprocessor = ColumnTransformer([
    ("num", numeric_pipeline, numeric_features),
    ("cat", categorical_pipeline, categorical_features),
])

model = Pipeline([
    ("preprocessor", preprocessor),
    ("classifier", RandomForestClassifier(n_estimators=100, random_state=42)),
])

# Train + predict in one call
model.fit(X_train, y_train)
predictions = model.predict(X_test)
```

**Interview insight:** Using `Pipeline` ensures that preprocessing is applied consistently to train and test data — preventing data leakage.

## Rule 5: Reproducibility

```python
import random
import numpy as np

def set_seed(seed: int = 42):
    """Set all random seeds for reproducibility."""
    random.seed(seed)
    np.random.seed(seed)
    # For PyTorch:
    # torch.manual_seed(seed)
    # torch.cuda.manual_seed_all(seed)
    # torch.backends.cudnn.deterministic = True

set_seed(42)
```

## Rule 6: Logging, Not Print

```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s - %(name)s - %(levelname)s - %(message)s"
)
logger = logging.getLogger(__name__)

logger.info(f"Training started with {len(X_train)} samples")
logger.info(f"Model accuracy: {accuracy:.4f}")
logger.warning(f"Class imbalance detected: ratio = {ratio:.2f}")
```

## Rule 7: Pin Your Dependencies

```
# requirements.txt — ALWAYS pin versions
numpy==1.24.3
pandas==2.0.3
scikit-learn==1.3.0
xgboost==1.7.6
matplotlib==3.7.2
pyyaml==6.0.1
```

---

## Common Interview Questions

1. **Q: How do you make ML experiments reproducible?**
   > Set random seeds, pin library versions, use config files for hyperparameters, version control your data (DVC), log experiments (MLflow/W&B), and use sklearn Pipelines to ensure consistent preprocessing.

2. **Q: Why use sklearn Pipelines instead of manual preprocessing?**
   > Pipelines apply transformations consistently to train and test data, prevent data leakage (e.g., fitting a scaler on test data), and make the model portable — you can serialize the entire pipeline.

---

## Resources

- 📖 [Scikit-learn Pipeline Guide](https://scikit-learn.org/stable/modules/compose.html)
- 📖 [Google's ML Engineering Best Practices](https://developers.google.com/machine-learning/guides/rules-of-ml)
- 📖 [Cookiecutter Data Science (project template)](https://drivendata.github.io/cookiecutter-data-science/)
]]>
