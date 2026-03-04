<![CDATA[# Matplotlib & Seaborn — Visualization for ML

> **Interview weight:** ⭐⭐ — Rarely tested directly, but essential for EDA and presenting results.  
> **Time to study:** 3–4 hours.  
> **Goal:** Produce clear, informative plots that tell a data story quickly.

---

## The 8 Plots Every ML Engineer Must Know

### 1. Distribution Plot — "What does the data look like?"

```python
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np

data = np.random.randn(1000)

fig, axes = plt.subplots(1, 2, figsize=(12, 4))
axes[0].hist(data, bins=30, edgecolor="black", alpha=0.7)
axes[0].set_title("Histogram")
sns.kdeplot(data, ax=axes[1], fill=True)
axes[1].set_title("KDE Plot")
plt.tight_layout()
plt.show()
```

**When to use:** First thing in EDA — check for skewness, bimodality, outliers.

### 2. Box Plot — "Where are the outliers?"

```python
import pandas as pd

df = pd.DataFrame({"group": ["A"]*100 + ["B"]*100,
                    "value": np.concatenate([np.random.randn(100), np.random.randn(100) + 2])})

sns.boxplot(x="group", y="value", data=df)
plt.title("Distribution by Group")
plt.show()
```

### 3. Scatter Plot — "Are these two features related?"

```python
plt.scatter(df["feature_1"], df["feature_2"], c=df["target"], cmap="coolwarm", alpha=0.6)
plt.colorbar(label="Target")
plt.xlabel("Feature 1")
plt.ylabel("Feature 2")
plt.title("Feature Relationship")
plt.show()
```

### 4. Correlation Heatmap — "Which features are correlated?"

```python
corr = df.select_dtypes(include=[np.number]).corr()
sns.heatmap(corr, annot=True, cmap="RdBu_r", center=0, fmt=".2f")
plt.title("Feature Correlation Matrix")
plt.show()
```

**Interview insight:** High correlation between features → multicollinearity → remove one or use regularization.

### 5. Pair Plot — "Show me everything at once"

```python
sns.pairplot(df, hue="target", diag_kind="kde")
plt.show()
```

### 6. Confusion Matrix — "How is my classifier performing?"

```python
from sklearn.metrics import confusion_matrix, ConfusionMatrixDisplay

cm = confusion_matrix(y_true, y_pred)
disp = ConfusionMatrixDisplay(cm, display_labels=["Negative", "Positive"])
disp.plot(cmap="Blues")
plt.title("Confusion Matrix")
plt.show()
```

### 7. ROC Curve — "How does my model trade off precision and recall?"

```python
from sklearn.metrics import roc_curve, auc

fpr, tpr, thresholds = roc_curve(y_true, y_prob)
roc_auc = auc(fpr, tpr)

plt.plot(fpr, tpr, label=f"AUC = {roc_auc:.3f}")
plt.plot([0, 1], [0, 1], "k--", label="Random")
plt.xlabel("False Positive Rate")
plt.ylabel("True Positive Rate")
plt.title("ROC Curve")
plt.legend()
plt.show()
```

### 8. Learning Curves — "Is my model overfitting?"

```python
from sklearn.model_selection import learning_curve

train_sizes, train_scores, val_scores = learning_curve(
    model, X, y, cv=5, train_sizes=np.linspace(0.1, 1.0, 10), scoring="accuracy"
)

plt.plot(train_sizes, train_scores.mean(axis=1), label="Train")
plt.plot(train_sizes, val_scores.mean(axis=1), label="Validation")
plt.xlabel("Training Set Size")
plt.ylabel("Accuracy")
plt.title("Learning Curves")
plt.legend()
plt.show()
```

**Interview insight:** If train and val curves diverge → overfitting (need regularization or more data). If both are low → underfitting (need a more complex model).

---

## Professional Plot Formatting

```python
# Always set a clean style
plt.style.use("seaborn-v0_8-whitegrid")

# Use consistent figure sizes
fig, ax = plt.subplots(figsize=(8, 5))

# Always label axes and add titles
ax.set_xlabel("Feature Name", fontsize=12)
ax.set_ylabel("Target", fontsize=12)
ax.set_title("Descriptive Title", fontsize=14, fontweight="bold")

# Save in high resolution for reports
plt.savefig("figure.png", dpi=300, bbox_inches="tight")
```

---

## Resources

- 📖 [Matplotlib Cheat Sheet](https://matplotlib.org/cheatsheets/)
- 📖 [Seaborn Gallery](https://seaborn.pydata.org/examples/index.html)
]]>
