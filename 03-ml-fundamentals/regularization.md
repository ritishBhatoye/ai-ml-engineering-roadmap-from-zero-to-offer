<![CDATA[# Regularization — Preventing Overfitting

> **Interview weight:** ⭐⭐⭐⭐ — Interviewers love connecting regularization to Bayesian priors and bias-variance.  
> **Time to study:** 4–5 hours.

---

## Why Regularization Exists

Models with too many parameters can memorize training data (overfit). Regularization adds a penalty on model complexity to the loss function.

```
Regularized Loss = Original Loss + λ · Complexity Penalty
```

---

## L1 Regularization (Lasso)

**Penalty:** λ · Σ|wᵢ|

**Effect:** Drives some weights to **exactly zero** → automatic feature selection.

```python
from sklearn.linear_model import Lasso

model = Lasso(alpha=0.1)  # alpha = λ
model.fit(X_train, y_train)
print(f"Non-zero coefficients: {(model.coef_ != 0).sum()} / {len(model.coef_)}")
```

**When to use:** When you suspect many features are irrelevant. L1 naturally selects the important ones.

## L2 Regularization (Ridge)

**Penalty:** λ · Σwᵢ²

**Effect:** Shrinks all weights toward zero (but never exactly zero) → smoother model.

```python
from sklearn.linear_model import Ridge

model = Ridge(alpha=1.0)
model.fit(X_train, y_train)
```

**When to use:** When all features might be relevant but you want to prevent large weights (multicollinearity).

## Elastic Net

**Combines L1 and L2:** λ₁ · Σ|wᵢ| + λ₂ · Σwᵢ²

```python
from sklearn.linear_model import ElasticNet

model = ElasticNet(alpha=0.1, l1_ratio=0.5)  # l1_ratio = λ₁/(λ₁+λ₂)
```

## The Bayesian Connection

| Regularization | Equivalent Prior | Effect |
|---|---|---|
| **L2 (Ridge)** | Gaussian prior on weights | Weights are likely small but non-zero |
| **L1 (Lasso)** | Laplacian prior on weights | Weights are likely exactly zero (sparse) |

This is the MLE vs MAP connection: regularization = MAP with a prior on the parameters.

## Regularization in Neural Networks

### Dropout

Randomly zero out neurons during training (typically 20–50%).

```python
import torch.nn as nn

model = nn.Sequential(
    nn.Linear(100, 64),
    nn.ReLU(),
    nn.Dropout(0.3),     # Drop 30% of neurons
    nn.Linear(64, 32),
    nn.ReLU(),
    nn.Dropout(0.3),
    nn.Linear(32, 1),
)
```

**Why it works:** Forces the network to not rely on any single neuron → distributes knowledge → reduces overfitting.

### Early Stopping

Stop training when validation loss starts increasing.

```python
# In PyTorch: track validation loss, stop when it increases for N epochs
best_val_loss = float("inf")
patience = 10
counter = 0

for epoch in range(1000):
    train_loss = train_one_epoch(model, train_loader)
    val_loss = evaluate(model, val_loader)
    
    if val_loss < best_val_loss:
        best_val_loss = val_loss
        counter = 0
        torch.save(model.state_dict(), "best_model.pt")  # Save best
    else:
        counter += 1
        if counter >= patience:
            print(f"Early stopping at epoch {epoch}")
            break
```

### Batch Normalization

Normalizes layer inputs → stabilizes training → acts as mild regularizer.

### Weight Decay

L2 regularization applied directly to optimizer:

```python
optimizer = torch.optim.Adam(model.parameters(), lr=0.001, weight_decay=1e-4)
```

---

## Choosing λ (Regularization Strength)

```python
from sklearn.linear_model import RidgeCV

# Automatically selects best alpha via cross-validation
model = RidgeCV(alphas=[0.01, 0.1, 1.0, 10.0, 100.0], cv=5)
model.fit(X_train, y_train)
print(f"Best alpha: {model.alpha_}")
```

---

## Common Interview Questions

1. **Q: Compare L1 and L2 regularization.**
   > L1 adds absolute value of weights as penalty → produces sparse models (feature selection). L2 adds squared weights → shrinks all weights evenly. L1 has a Laplacian prior, L2 has a Gaussian prior. Use L1 when feature selection is needed, L2 when all features matter.

2. **Q: Why does dropout work?**
   > It creates an implicit ensemble of sub-networks. Each training step uses a different sub-network. At inference, the full network (with scaled weights) approximates the ensemble average.

3. **Q: How does early stopping relate to regularization?**
   > Early stopping limits the effective capacity of the model by stopping before it can fully memorize the training data. The number of training steps acts as an implicit regularization parameter — fewer steps = stronger regularization.

---

## Resources

- 📺 [StatQuest — Ridge, Lasso, Elastic Net](https://www.youtube.com/c/joshstarmer)
- 📖 [Hands-On ML — Chapter 4 (Regularized Models)](https://github.com/ageron/handson-ml2)
]]>
