<![CDATA[# Supervised Learning — The Core of ML Interviews

> **Interview weight:** ⭐⭐⭐⭐⭐ — This is the most heavily tested topic.  
> **Time to study:** 8–10 hours.  
> **Goal:** Deeply understand every major supervised algorithm, when to use it, and its tradeoffs.

---

## The Big Picture

Supervised learning: given labeled data (X, y), learn a function f(X) → y.

| Problem Type | Target y | Loss Function | Evaluation Metrics |
|---|---|---|---|
| **Regression** | Continuous (price, temperature) | MSE, MAE, Huber | RMSE, MAE, R² |
| **Classification** | Discrete (spam/not spam) | Cross-entropy, hinge | Accuracy, Precision, Recall, F1, AUC |

---

## 1. Linear Regression

**Model:** y = Xw + b

**Closed-form solution:** w = (XᵀX)⁻¹Xᵀy

**Gradient descent update:** w ← w − α · (2/n) · Xᵀ(Xw − y)

```python
import numpy as np
from sklearn.linear_model import LinearRegression

# From scratch
class LinearRegressionScratch:
    def fit(self, X, y, lr=0.01, epochs=1000):
        n, d = X.shape
        self.w = np.zeros(d)
        self.b = 0
        
        for _ in range(epochs):
            y_pred = X @ self.w + self.b
            error = y_pred - y
            self.w -= lr * (2/n) * (X.T @ error)
            self.b -= lr * (2/n) * error.sum()
    
    def predict(self, X):
        return X @ self.w + self.b

# With sklearn (production use)
model = LinearRegression()
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
```

**Assumptions:** Linear relationship, no multicollinearity, homoscedasticity, normally distributed residuals.

**Interview Q: When does linear regression fail?**
> When the relationship is non-linear, when features are highly correlated (multicollinearity), when there are outliers (use robust regression), or when features outnumber samples (use regularization).

---

## 2. Logistic Regression

**Not** a regression algorithm — it's a classifier.

**Model:** P(y=1|X) = σ(Xw + b), where σ(z) = 1/(1+e⁻ᶻ)

**Loss:** Binary Cross-Entropy = −(1/n) Σ [yᵢ log(ŷᵢ) + (1−yᵢ) log(1−ŷᵢ)]

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression(C=1.0, penalty="l2", max_iter=1000)
model.fit(X_train, y_train)

# Probabilities (for ROC-AUC)
y_prob = model.predict_proba(X_test)[:, 1]

# Hard predictions (for accuracy, F1)
y_pred = model.predict(X_test)
```

**Interview Q: Explain the decision boundary of logistic regression.**
> The decision boundary is where P(y=1|X) = 0.5, i.e., Xw + b = 0. It's a hyperplane in feature space. Can only model linear boundaries — for non-linear, use polynomial features or switch to a non-linear model.

**Interview Q: What does the C parameter do?**
> C = 1/λ (inverse of regularization strength). Small C → strong regularization → simpler model. Large C → weak regularization → complex model. Default is 1.0.

---

## 3. k-Nearest Neighbors (k-NN)

**Idea:** For a new point, find the k closest training points and vote (classification) or average (regression).

**No training phase** — all computation happens at prediction time (lazy learner).

```python
from sklearn.neighbors import KNeighborsClassifier

model = KNeighborsClassifier(n_neighbors=5, metric="minkowski", p=2)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
```

**Key tradeoffs:**

| Factor | Effect |
|---|---|
| **k too small** | Noisy, overfits (captures noise) |
| **k too large** | Smooth, underfits (loses local structure) |
| **Features not scaled** | Features with larger range dominate distance |
| **High dimensions** | "Curse of dimensionality" — distances become meaningless |

**Interview Q: Why doesn't k-NN work well in high dimensions?**
> In high-dimensional space, all points become roughly equidistant. The concept of "nearest" loses meaning. You need to reduce dimensions (PCA) or use a different algorithm.

---

## 4. Decision Trees

**Idea:** Recursively split the data on a feature threshold that best separates the classes.

**Splitting criteria:**
- Classification: Gini impurity, entropy (information gain)
- Regression: MSE reduction

```python
from sklearn.tree import DecisionTreeClassifier

model = DecisionTreeClassifier(max_depth=5, min_samples_split=10, random_state=42)
model.fit(X_train, y_train)
```

**Gini impurity:** Gini(t) = 1 − Σ pᵢ², where pᵢ is the proportion of class i in node t.

**Information gain:** IG = H(parent) − Σ (nᵢ/N) · H(childᵢ), where H is entropy.

**Pros:** Interpretable, handles non-linear relationships, no feature scaling needed.  
**Cons:** Prone to overfitting (high variance), unstable (small data changes → different tree).

**Interview Q: How do you prevent a decision tree from overfitting?**
> (1) Limit max_depth, (2) Require minimum samples per leaf/split, (3) Prune after training, (4) Use ensembles (Random Forest) to average out variance.

---

## 5. Random Forest

An ensemble of decision trees, each trained on a random bootstrap sample and a random subset of features.

```python
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier(
    n_estimators=200,      # Number of trees
    max_depth=10,          # Limit depth per tree
    max_features="sqrt",   # Features per split = √(total features)
    min_samples_leaf=5,    # Minimum samples in a leaf
    random_state=42,
    n_jobs=-1,             # Use all CPU cores
)
model.fit(X_train, y_train)

# Feature importance
importances = model.feature_importances_
```

**Why it works:** Each tree overfits differently. Averaging many overfit trees → reduces variance → better generalization.

**Interview Q: What's the difference between bagging and boosting?**
> **Bagging** (Random Forest): Train trees independently on bootstrap samples, aggregate by voting/averaging. Reduces variance.  
> **Boosting** (XGBoost): Train trees sequentially, each correcting the previous tree's errors. Reduces bias AND variance.

---

## 6. Gradient Boosting (XGBoost / LightGBM)

The go-to algorithm for tabular data competitions and industry applications.

```python
import xgboost as xgb

model = xgb.XGBClassifier(
    n_estimators=300,
    max_depth=6,
    learning_rate=0.1,
    subsample=0.8,
    colsample_bytree=0.8,
    reg_alpha=0.1,      # L1 regularization
    reg_lambda=1.0,     # L2 regularization
    use_label_encoder=False,
    eval_metric="logloss",
    random_state=42,
)

model.fit(
    X_train, y_train,
    eval_set=[(X_val, y_val)],
    verbose=50,
)
```

**Key hyperparameters:**

| Parameter | Effect | Tuning Range |
|---|---|---|
| `n_estimators` | Number of boosting rounds | 100–1000 |
| `max_depth` | Tree depth (controls complexity) | 3–10 |
| `learning_rate` | Step size (lower = more trees needed) | 0.01–0.3 |
| `subsample` | Fraction of samples per tree | 0.6–1.0 |
| `reg_alpha` / `reg_lambda` | L1/L2 regularization | 0–10 |

**Interview Q: Walk me through how XGBoost builds each tree.**
> (1) Compute residuals (errors) from the current ensemble. (2) Fit a new tree to predict those residuals. (3) Add the new tree's predictions (scaled by learning rate) to the ensemble. (4) Repeat. Each tree corrects the errors of the previous ensemble.

---

## 7. Support Vector Machines (SVM)

**Idea:** Find the hyperplane that maximizes the margin between classes.

```python
from sklearn.svm import SVC

model = SVC(kernel="rbf", C=1.0, gamma="scale")
model.fit(X_train, y_train)
```

**Kernels:** Linear, polynomial, RBF (Gaussian). The kernel trick maps data to higher dimensions without computing the transformation explicitly.

**When to use:** Small-to-medium datasets, high-dimensional data (e.g., text classification). Don't use for large datasets (training is O(n²) to O(n³)).

---

## Algorithm Selection Cheat Sheet

```
Start here:
│
├── Tabular data?
│   ├── < 10K samples → Try Logistic Regression, SVM, Random Forest
│   ├── > 10K samples → XGBoost / LightGBM (almost always)
│   └── Need interpretability? → Decision Tree or Logistic Regression
│
├── Text data? → TF-IDF + Logistic Regression (baseline), then BERT
│
├── Image data? → CNN (PyTorch/TensorFlow)
│
└── Time series? → ARIMA (baseline), then LSTM/Transformer
```

---

## Common Interview Questions

1. **Q: Compare Random Forest and XGBoost.**
   > RF trains trees independently (bagging), XGBoost trains sequentially (boosting). RF reduces variance, XGBoost reduces bias and variance. XGBoost usually achieves better accuracy but is more prone to overfitting if not tuned. RF is simpler to tune and more robust.

2. **Q: When would you use logistic regression over XGBoost?**
   > When interpretability is important (healthcare, finance), when the dataset is small, when you need calibrated probabilities, or when speed at inference matters. Logistic regression is also a strong baseline — always start there.

3. **Q: What's the difference between hard and soft voting in ensembles?**
   > Hard voting: each model votes for a class, majority wins. Soft voting: average the predicted probabilities, choose highest. Soft voting is usually better because it uses confidence information.

---

## Try It Yourself

1. Implement logistic regression from scratch using gradient descent. Compare with sklearn.
2. Train 5 different models on the same dataset. Build a comparison table with accuracy, F1, AUC, and training time.
3. Build an XGBoost pipeline with hyperparameter tuning (RandomizedSearchCV). Plot feature importances.

---

## Resources

- 📖 [Hands-On ML — Chapters 4, 5, 6, 7](https://github.com/ageron/handson-ml2)
- 📺 [StatQuest — Decision Trees, Random Forests, XGBoost](https://www.youtube.com/c/joshstarmer)
- 📖 [XGBoost Documentation](https://xgboost.readthedocs.io/)
]]>
