<![CDATA[# Case Study: Credit Risk Model

> **Interview relevance:** Tests imbalanced data handling, interpretability, and regulatory awareness.

---

## Problem Statement

Predict whether a loan applicant will default within 12 months.

## Key Challenges

### 1. Class Imbalance

Defaults are rare (2-5% of applications). Accuracy is useless.

```python
from imblearn.over_sampling import SMOTE
from sklearn.utils.class_weight import compute_class_weight

# Option 1: Class weights
weights = compute_class_weight('balanced', classes=np.unique(y), y=y)
model = XGBClassifier(scale_pos_weight=weights[1]/weights[0])

# Option 2: SMOTE (oversample minority class)
smote = SMOTE(random_state=42)
X_resampled, y_resampled = smote.fit_resample(X_train, y_train)

# Option 3: Adjust threshold (most practical)
y_prob = model.predict_proba(X_test)[:, 1]
y_pred = (y_prob >= 0.3).astype(int)  # Lower threshold → catch more defaults
```

### 2. Feature Engineering

```python
# Key features for credit risk
features = {
    'debt_to_income': loan_amount / annual_income,
    'credit_utilization': total_balance / total_credit_limit,
    'payment_history_score': on_time_payments / total_payments,
    'account_age_months': months_since_oldest_account,
    'recent_inquiries': hard_inquiries_last_6m,
}
```

### 3. Model Interpretability (Required in Finance)

```python
import shap

explainer = shap.TreeExplainer(model)
shap_values = explainer.shap_values(X_test)
shap.summary_plot(shap_values, X_test, feature_names=feature_names)

# For individual predictions:
shap.force_plot(explainer.expected_value, shap_values[0], X_test.iloc[0])
```

### 4. Evaluation

- **Primary:** AUC-ROC (threshold-independent ranking)
- **Business:** KS statistic, Gini coefficient
- **At threshold:** Precision at 95% recall (catch most defaults)

## Production Considerations

- **Regulatory compliance:** Model must be explainable (no black boxes)
- **Fairness:** Check for bias across protected attributes (race, gender, age)
- **Monitoring:** Track approval rate, default rate, and model PSI monthly
- **Temporal validation:** Train on past data, validate on future periods (no random split)

## Interview Questions

1. How do you handle the 95/5 class imbalance?
2. Why can't you use random train/test split for credit data?
3. How would you explain a model decision to a rejected applicant?
4. What metrics would you monitor after deployment?
]]>
