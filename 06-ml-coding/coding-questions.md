<![CDATA[# ML Coding Interview Questions

> **Interview weight:** ⭐⭐⭐⭐ — You will be asked to implement ML algorithms from scratch.  
> **Time to study:** 8–10 hours (practice, practice, practice).

---

## Category 1: Implement from Scratch (NumPy Only)

### Q1. Linear Regression with Gradient Descent

```python
import numpy as np

class LinearRegression:
    def fit(self, X, y, lr=0.01, epochs=1000):
        n, d = X.shape
        self.w = np.zeros(d)
        self.b = 0.0
        for _ in range(epochs):
            y_pred = X @ self.w + self.b
            dw = (2/n) * X.T @ (y_pred - y)
            db = (2/n) * np.sum(y_pred - y)
            self.w -= lr * dw
            self.b -= lr * db
    
    def predict(self, X):
        return X @ self.w + self.b
```

### Q2. Logistic Regression

```python
class LogisticRegression:
    def _sigmoid(self, z):
        return 1 / (1 + np.exp(-np.clip(z, -500, 500)))
    
    def fit(self, X, y, lr=0.01, epochs=1000):
        n, d = X.shape
        self.w = np.zeros(d)
        self.b = 0.0
        for _ in range(epochs):
            z = X @ self.w + self.b
            y_pred = self._sigmoid(z)
            dw = (1/n) * X.T @ (y_pred - y)
            db = (1/n) * np.sum(y_pred - y)
            self.w -= lr * dw
            self.b -= lr * db
    
    def predict_proba(self, X):
        return self._sigmoid(X @ self.w + self.b)
    
    def predict(self, X, threshold=0.5):
        return (self.predict_proba(X) >= threshold).astype(int)
```

### Q3. K-Nearest Neighbors

```python
class KNN:
    def __init__(self, k=5):
        self.k = k
    
    def fit(self, X, y):
        self.X_train = X
        self.y_train = y
    
    def predict(self, X):
        predictions = []
        for x in X:
            distances = np.linalg.norm(self.X_train - x, axis=1)
            k_indices = np.argsort(distances)[:self.k]
            k_labels = self.y_train[k_indices]
            # Majority vote
            values, counts = np.unique(k_labels, return_counts=True)
            predictions.append(values[np.argmax(counts)])
        return np.array(predictions)
```

### Q4. K-Means Clustering

```python
class KMeans:
    def __init__(self, k=3, max_iters=100):
        self.k = k
        self.max_iters = max_iters
    
    def fit(self, X):
        idx = np.random.choice(len(X), self.k, replace=False)
        self.centroids = X[idx].copy()
        
        for _ in range(self.max_iters):
            distances = np.linalg.norm(X[:, None] - self.centroids, axis=2)
            self.labels = np.argmin(distances, axis=1)
            new_centroids = np.array([X[self.labels == i].mean(axis=0) for i in range(self.k)])
            if np.allclose(self.centroids, new_centroids):
                break
            self.centroids = new_centroids
        return self
```

### Q5. Decision Tree (Simplified)

```python
class DecisionTreeNode:
    def __init__(self, feature=None, threshold=None, left=None, right=None, value=None):
        self.feature = feature
        self.threshold = threshold
        self.left = left
        self.right = right
        self.value = value  # Leaf prediction

def gini(y):
    classes, counts = np.unique(y, return_counts=True)
    p = counts / len(y)
    return 1 - np.sum(p ** 2)

def best_split(X, y):
    best_gini, best_feat, best_thresh = float("inf"), None, None
    for feat in range(X.shape[1]):
        thresholds = np.unique(X[:, feat])
        for thresh in thresholds:
            left_mask = X[:, feat] <= thresh
            if left_mask.sum() == 0 or (~left_mask).sum() == 0:
                continue
            g = (left_mask.sum() * gini(y[left_mask]) + 
                 (~left_mask).sum() * gini(y[~left_mask])) / len(y)
            if g < best_gini:
                best_gini, best_feat, best_thresh = g, feat, thresh
    return best_feat, best_thresh
```

---

## Category 2: Utility Functions

### Q6. Compute Confusion Matrix

```python
def confusion_matrix(y_true, y_pred):
    classes = np.unique(np.concatenate([y_true, y_pred]))
    n = len(classes)
    cm = np.zeros((n, n), dtype=int)
    for t, p in zip(y_true, y_pred):
        cm[t][p] += 1
    return cm
```

### Q7. Precision, Recall, F1

```python
def precision_recall_f1(y_true, y_pred):
    tp = np.sum((y_true == 1) & (y_pred == 1))
    fp = np.sum((y_true == 0) & (y_pred == 1))
    fn = np.sum((y_true == 1) & (y_pred == 0))
    precision = tp / (tp + fp) if (tp + fp) > 0 else 0
    recall = tp / (tp + fn) if (tp + fn) > 0 else 0
    f1 = 2 * precision * recall / (precision + recall) if (precision + recall) > 0 else 0
    return precision, recall, f1
```

### Q8. Softmax

```python
def softmax(z):
    exp_z = np.exp(z - np.max(z))  # Numerical stability
    return exp_z / exp_z.sum(axis=-1, keepdims=True)
```

### Q9. Cross-Entropy Loss

```python
def cross_entropy(y_true, y_pred_proba):
    eps = 1e-15
    y_pred_proba = np.clip(y_pred_proba, eps, 1 - eps)
    return -np.mean(y_true * np.log(y_pred_proba) + (1 - y_true) * np.log(1 - y_pred_proba))
```

### Q10. Cosine Similarity

```python
def cosine_similarity(a, b):
    return np.dot(a, b) / (np.linalg.norm(a) * np.linalg.norm(b))
```

---

## Category 3: Data Manipulation

### Q11. Normalize a dataset (zero mean, unit variance)
### Q12. Implement one-hot encoding without sklearn
### Q13. Implement train-test split with stratification
### Q14. Implement k-fold cross-validation
### Q15. Write a function to detect and remove outliers (IQR method)

---

## Category 4: Probability & Stats Coding

### Q16. Simulate the Monty Hall problem (10,000 trials)
### Q17. Implement a bootstrap confidence interval for the mean
### Q18. Estimate π using Monte Carlo simulation
### Q19. Implement a simple A/B test (z-test for proportions)
### Q20. Sample from a discrete distribution using inverse CDF

---

## Practice Strategy

1. **Week 1:** Implement Q1–Q5 from scratch. Debug until they match sklearn output.
2. **Week 2:** Implement Q6–Q10. Use them in your projects.
3. **Week 3:** Attempt Q11–Q20 without looking at solutions.
4. **Week 4:** Time yourself — can you implement logistic regression in 15 minutes?

---

## Resources

- 💻 [ML-From-Scratch GitHub](https://github.com/eriklindernoren/ML-From-Scratch)
- 📖 [Scikit-learn source code](https://github.com/scikit-learn/scikit-learn) — study how the pros implement it
]]>
