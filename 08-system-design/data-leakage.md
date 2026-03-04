<![CDATA[# Data Leakage — The Silent Model Killer

> **Interview weight:** ⭐⭐⭐⭐⭐ — Interviewers specifically test for leakage awareness.

---

## What Is Data Leakage?

Data leakage occurs when information from outside the training data is used to create the model, leading to **unrealistically good performance** that doesn't generalize to production.

A model with leakage might show 99% accuracy in development and 55% in production.

---

## Types of Data Leakage

### 1. Target Leakage
Using a feature that is a **consequence** of the target (not available at prediction time).

**Example:** Predicting hospital readmission using "discharge medication" — this is assigned AFTER the readmission happens.

**Fix:** For every feature, ask: "Would I have this information at the time I need to make a prediction?"

### 2. Train-Test Contamination
Preprocessing steps fit on the full dataset (including test data).

```python
# BAD — scaler sees test data
scaler.fit(X_all)
X_train = scaler.transform(X_train)
X_test = scaler.transform(X_test)

# GOOD — scaler only sees training data
scaler.fit(X_train)
X_train = scaler.transform(X_train)
X_test = scaler.transform(X_test)
```

### 3. Temporal Leakage
Using future data to predict the past.

**Example:** Predicting stock prices on Day 5 using moving averages computed over Days 1-10.

**Fix:** Use temporal (time-based) train/test splits. Never use future-looking features.

### 4. Group Leakage
Data from the same entity (patient, user) appears in both train and test.

**Fix:** Use `GroupKFold` to ensure all data from one group stays in one split.

```python
from sklearn.model_selection import GroupKFold

gkf = GroupKFold(n_splits=5)
for train_idx, test_idx in gkf.split(X, y, groups=user_ids):
    # All data from a user is in train OR test, never both
    pass
```

---

## How to Detect Leakage

1. **Suspiciously high performance** — If accuracy is 99%+, question it
2. **Feature importance check** — If one feature dominates, investigate whether it's valid
3. **Production performance gap** — Model works in offline evaluation but fails live
4. **Temporal validation** — Train on past, test on future. If score drops significantly, leakage is likely

---

## Prevention Checklist

- [ ] Split data BEFORE any preprocessing
- [ ] Use sklearn Pipeline for all transformations
- [ ] For time-series, use temporal splits only
- [ ] Check that no feature is derived from the target
- [ ] Use GroupKFold when data has entity-level grouping
- [ ] Validate on a truly unseen holdout set
]]>
