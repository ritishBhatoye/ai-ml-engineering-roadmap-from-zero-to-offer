<![CDATA[# Evaluation Metrics — Measuring What Matters

> **Interview weight:** ⭐⭐⭐⭐⭐ — You WILL be asked "Why did you choose this metric?"  
> **Time to study:** 4–5 hours.

---

## Classification Metrics

### The Confusion Matrix

```
                  Predicted
                  Pos    Neg
Actual  Pos  │  TP   │  FN   │
        Neg  │  FP   │  TN   │
```

```python
from sklearn.metrics import confusion_matrix, classification_report

cm = confusion_matrix(y_true, y_pred)
print(classification_report(y_true, y_pred))
```

### Core Metrics

| Metric | Formula | When to Use |
|---|---|---|
| **Accuracy** | (TP+TN) / (TP+TN+FP+FN) | Balanced classes ONLY |
| **Precision** | TP / (TP+FP) | When false positives are costly (spam filter) |
| **Recall (Sensitivity)** | TP / (TP+FN) | When false negatives are costly (disease detection) |
| **F1 Score** | 2·P·R / (P+R) | When you need to balance precision and recall |
| **Specificity** | TN / (TN+FP) | When true negative rate matters |

**Interview Q: Your spam classifier has 95% accuracy but users are complaining. What's wrong?**
> If only 5% of emails are spam, a model that predicts "not spam" for everything gets 95% accuracy. The problem is: precision and recall on the spam class are 0%. **Accuracy is misleading with imbalanced classes** — use F1 or AUC instead.

### ROC-AUC

**ROC curve:** Plots True Positive Rate vs False Positive Rate at various thresholds.

**AUC:** Area under the ROC curve (0.5 = random, 1.0 = perfect).

```python
from sklearn.metrics import roc_auc_score, roc_curve

# Need probability scores, not hard predictions!
y_prob = model.predict_proba(X_test)[:, 1]
auc = roc_auc_score(y_true, y_prob)
```

**When to use:** Binary classification, especially when you want a threshold-independent metric.

**When NOT to use:** Highly imbalanced data — use **Precision-Recall AUC** instead.

### Precision-Recall Curve

Better than ROC for imbalanced datasets (fraud detection, rare disease).

```python
from sklearn.metrics import precision_recall_curve, average_precision_score

precision, recall, thresholds = precision_recall_curve(y_true, y_prob)
ap = average_precision_score(y_true, y_prob)
```

### Log Loss (Cross-Entropy)

Measures how well predicted probabilities match true labels. Lower is better.

```python
from sklearn.metrics import log_loss

ll = log_loss(y_true, y_prob)
```

**When to use:** When you care about the quality of probability estimates (not just the predicted class).

---

## Regression Metrics

| Metric | Formula | Interpretation |
|---|---|---|
| **MSE** | (1/n) Σ(yᵢ - ŷᵢ)² | Penalizes large errors heavily |
| **RMSE** | √MSE | Same units as target |
| **MAE** | (1/n) Σ\|yᵢ - ŷᵢ\| | Robust to outliers |
| **R²** | 1 - (SS_res / SS_tot) | Proportion of variance explained (0-1) |
| **MAPE** | (1/n) Σ\|yᵢ - ŷᵢ\|/\|yᵢ\| | Percentage error (interpretable) |

```python
from sklearn.metrics import mean_squared_error, mean_absolute_error, r2_score
import numpy as np

mse = mean_squared_error(y_true, y_pred)
rmse = np.sqrt(mse)
mae = mean_absolute_error(y_true, y_pred)
r2 = r2_score(y_true, y_pred)
```

**Interview Q: When would you use MAE over MSE?**
> MAE is robust to outliers (linear penalty). MSE penalizes large errors quadratically. If your data has outliers and you don't want them to dominate the loss, use MAE. If large errors are especially undesirable (e.g., predicting house prices — a $100K error is worse than two $50K errors), use MSE.

---

## Choosing the Right Metric

| Scenario | Recommended Metric | Reason |
|---|---|---|
| **Balanced binary classification** | F1, AUC-ROC | Balanced view of precision and recall |
| **Imbalanced classes** | F1, PR-AUC | ROC-AUC can be misleadingly high |
| **Fraud/disease detection** | Recall (at acceptable precision) | Missing a fraud case is very costly |
| **Spam filtering** | Precision (at acceptable recall) | Blocking a real email is very costly |
| **Regression with outliers** | MAE | Robust to extreme values |
| **Regression, business use** | MAPE | Intuitive: "5% average error" |
| **Probability calibration** | Log loss (Brier score) | Measures probability quality |
| **Ranking (recommendations)** | NDCG, MAP@K | Position-sensitive evaluation |

---

## Multi-Class Metrics

```python
from sklearn.metrics import classification_report

# Averaging strategies for multi-class:
# macro: simple average across classes (treats all classes equally)
# weighted: weighted by class support (accounts for imbalance)
# micro: aggregate TP/FP/FN across all classes

print(classification_report(y_true, y_pred))
```

**Interview Q: What's the difference between macro and weighted F1?**
> **Macro:** Compute F1 for each class, then average. Treats rare classes equally — use when all classes matter. **Weighted:** Compute F1 for each class, then average weighted by class support. Use when you want the overall metric to reflect class distribution.

---

## Common Interview Questions

1. **Q: A model has AUC = 0.95 but F1 = 0.30. How is this possible?**
   > AUC evaluates across ALL thresholds. F1 is computed at a specific threshold (default 0.5). If the classes are imbalanced, 0.5 may be a poor threshold. Adjusting the threshold (e.g., to 0.3) might dramatically improve F1.

2. **Q: Can accuracy be a good metric? When?**
   > Yes — when classes are balanced AND the cost of false positives and false negatives is roughly equal. For most real-world problems (imbalanced data, asymmetric costs), accuracy is misleading.

3. **Q: Explain the precision-recall tradeoff.**
   > Lowering the classification threshold → more positive predictions → recall increases (catch more positives) but precision decreases (more false positives). Raising the threshold → fewer positive predictions → precision increases but recall decreases.

---

## Resources

- 📺 [StatQuest — ROC and AUC](https://www.youtube.com/watch?v=4jRBRDbJemM)
- 📖 [Scikit-learn Metrics Guide](https://scikit-learn.org/stable/modules/model_evaluation.html)
]]>
