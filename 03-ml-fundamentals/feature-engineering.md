<![CDATA[# Feature Engineering — What Separates Good from Great ML Engineers

> **Interview weight:** ⭐⭐⭐⭐⭐ — Interviewers test this heavily because it reflects real-world experience.  
> **Time to study:** 6–8 hours.

---

## Why Feature Engineering Is the #1 Skill

> "Coming up with features is difficult, time-consuming, requires expert knowledge. Applied ML is basically feature engineering." — Andrew Ng

At top companies, the difference between a 0.82 and 0.90 AUC model is almost always better features, not a fancier algorithm.

---

## 1. Handling Missing Values

| Strategy | When to Use | Code |
|---|---|---|
| **Drop rows** | < 5% missing, missing at random | `df.dropna()` |
| **Mean/median imputation** | Numeric features, MCAR | `SimpleImputer(strategy="median")` |
| **Mode imputation** | Categorical features | `SimpleImputer(strategy="most_frequent")` |
| **Indicator variable** | Missingness itself is informative | `df["col_missing"] = df["col"].isnull().astype(int)` |
| **KNN imputation** | Complex patterns in missingness | `KNNImputer(n_neighbors=5)` |

**Interview insight:** Adding a binary "is_missing" column + imputing the value often outperforms imputation alone.

---

## 2. Encoding Categorical Variables

| Method | When to Use | Pitfalls |
|---|---|---|
| **One-Hot Encoding** | Low cardinality (< 15 categories) | Creates many sparse columns for high cardinality |
| **Label Encoding** | Ordinal categories (low/medium/high) | Imposes false ordering for nominal categories |
| **Target Encoding** | High cardinality (city, zip code) | **Must** use cross-validation to avoid leakage |
| **Frequency Encoding** | When cardinality matters | Loses information about the category identity |

```python
from sklearn.preprocessing import OneHotEncoder
from category_encoders import TargetEncoder

# One-hot (use for low cardinality)
ohe = OneHotEncoder(drop="first", sparse_output=False, handle_unknown="ignore")

# Target encoding (use for high cardinality with CV)
te = TargetEncoder(cols=["city"], smoothing=1.0)
# IMPORTANT: Fit on training data ONLY to prevent leakage
te.fit(X_train, y_train)
X_train_encoded = te.transform(X_train)
X_test_encoded = te.transform(X_test)
```

---

## 3. Feature Scaling

| Method | Formula | When to Use |
|---|---|---|
| **StandardScaler** | (x - μ) / σ | Most cases; required for SVM, logistic regression, k-NN |
| **MinMaxScaler** | (x - min) / (max - min) | When you need features in [0, 1] |
| **RobustScaler** | (x - median) / IQR | When data has outliers |
| **Log Transform** | log(1 + x) | Right-skewed distributions (income, prices) |

```python
from sklearn.preprocessing import StandardScaler, RobustScaler
import numpy as np

# Always fit on TRAINING data only, then transform both
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)  # NOT fit_transform!

# Log transform for skewed features
df["income_log"] = np.log1p(df["income"])  # log(1+x) handles zeros
```

**Interview Q: Do tree-based models need feature scaling?**
> No. Decision trees, random forests, and gradient boosting split on thresholds — scaling doesn't change the split points. Linear models, k-NN, SVM, and neural networks DO require scaling.

---

## 4. Creating New Features

### Date/Time Features

```python
df["day_of_week"] = df["timestamp"].dt.dayofweek     # Mon=0, Sun=6
df["hour"] = df["timestamp"].dt.hour
df["is_weekend"] = (df["day_of_week"] >= 5).astype(int)
df["month"] = df["timestamp"].dt.month
df["days_since_event"] = (pd.Timestamp.now() - df["event_date"]).dt.days
```

### Interaction Features

```python
df["price_per_sqft"] = df["price"] / df["square_feet"]
df["income_to_debt_ratio"] = df["income"] / (df["debt"] + 1)
df["bmi"] = df["weight"] / (df["height"] / 100) ** 2
```

### Aggregation Features

```python
# User-level features from transaction data
user_features = df.groupby("user_id").agg(
    total_spend=("amount", "sum"),
    avg_spend=("amount", "mean"),
    num_transactions=("amount", "count"),
    days_active=("date", lambda x: (x.max() - x.min()).days),
    most_common_category=("category", lambda x: x.mode()[0]),
)
```

### Binning / Discretization

```python
# Equal-width bins
df["age_group"] = pd.cut(df["age"], bins=[0, 18, 30, 50, 100], 
                          labels=["teen", "young", "middle", "senior"])

# Quantile bins (equal-frequency)
df["income_quartile"] = pd.qcut(df["income"], q=4, labels=False)
```

---

## 5. Feature Selection

### Method 1: Correlation Filter

```python
# Remove features with high correlation (> 0.95)
corr_matrix = df.corr().abs()
upper = corr_matrix.where(np.triu(np.ones(corr_matrix.shape), k=1).astype(bool))
to_drop = [col for col in upper.columns if any(upper[col] > 0.95)]
df.drop(columns=to_drop, inplace=True)
```

### Method 2: Feature Importance

```python
from sklearn.ensemble import RandomForestClassifier
import matplotlib.pyplot as plt

model = RandomForestClassifier(n_estimators=100, random_state=42)
model.fit(X_train, y_train)

importance = pd.Series(model.feature_importances_, index=feature_names)
importance.nlargest(20).plot(kind="barh")
plt.title("Top 20 Feature Importances")
plt.show()
```

### Method 3: Mutual Information

```python
from sklearn.feature_selection import mutual_info_classif

mi_scores = mutual_info_classif(X_train, y_train, random_state=42)
mi_series = pd.Series(mi_scores, index=feature_names).sort_values(ascending=False)
```

---

## 6. Data Leakage in Feature Engineering

⚠️ **The most common and dangerous mistake.**

| Type | Example | Fix |
|---|---|---|
| **Target leakage** | Using future information to predict the past | Strict temporal split; never use future features |
| **Train-test contamination** | Fitting a scaler on the full dataset, then splitting | Always `fit` on training data only |
| **Data snooping** | Looking at test data to guide feature decisions | Separate test set completely; use cross-validation |

**Interview Q: How do you prevent data leakage in feature engineering?**
> (1) Split data BEFORE any preprocessing. (2) Use `sklearn.Pipeline` to chain transformations with the model. (3) For time-series, use temporal splits only. (4) For target encoding, use cross-validated encoding. (5) Never use test data for any fitting or selection decision.

---

## Common Interview Questions

1. **Q: You have a categorical feature with 10,000 unique values. How do you encode it?**
   > Target encoding with cross-validation (to avoid leakage), or frequency encoding, or embeddings if using deep learning. One-hot encoding would create 10K sparse columns — impractical.

2. **Q: A feature has a right-skewed distribution. What do you do?**
   > Apply a log transform: `np.log1p(x)`. If there are zeros or negatives, use Box-Cox or Yeo-Johnson transforms. This helps linear models and also makes outliers less extreme.

3. **Q: How do you know which features to keep?**
   > Start with domain knowledge. Then use: (1) Correlation analysis (remove redundant features). (2) Feature importance from a tree model. (3) Mutual information scores. (4) Recursive Feature Elimination (RFE). Always validate that removing features doesn't hurt cross-validated performance.

---

## Resources

- 📖 [Feature Engineering and Selection (free book)](https://bookdown.org/max/FES/)
- 📖 [Kaggle Feature Engineering Course (free)](https://www.kaggle.com/learn/feature-engineering)
]]>
