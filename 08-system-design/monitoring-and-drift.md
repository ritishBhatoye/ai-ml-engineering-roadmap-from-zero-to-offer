<![CDATA[# Monitoring & Model Drift

> **Interview weight:** ⭐⭐⭐ — Shows production awareness beyond just training models.

---

## Types of Drift

| Type | What Changes | Example | Detection |
|---|---|---|---|
| **Data drift** | Input feature distributions shift | Customer demographics change after marketing campaign | PSI, KS test on features |
| **Concept drift** | Relationship between features and target changes | User buying patterns shift during COVID | Monitor prediction accuracy over time |
| **Label drift** | Target distribution changes | Fraud rate increases due to new attack vector | Track label distribution |

---

## Population Stability Index (PSI)

Measures how much a distribution has shifted from a reference (training) distribution.

```python
def calculate_psi(expected, actual, buckets=10):
    """Calculate PSI between two distributions."""
    breakpoints = np.percentile(expected, np.linspace(0, 100, buckets + 1))
    expected_counts = np.histogram(expected, breakpoints)[0] / len(expected)
    actual_counts = np.histogram(actual, breakpoints)[0] / len(actual)
    
    # Avoid log(0)
    expected_counts = np.clip(expected_counts, 1e-6, None)
    actual_counts = np.clip(actual_counts, 1e-6, None)
    
    psi = np.sum((actual_counts - expected_counts) * np.log(actual_counts / expected_counts))
    return psi
```

| PSI Value | Interpretation |
|---|---|
| < 0.1 | No significant change |
| 0.1 - 0.2 | Moderate change — investigate |
| > 0.2 | Significant change — retrain |

---

## What to Monitor

### Model Performance
- Accuracy, F1, AUC on labeled data (if available)
- Proxy metrics: confidence scores, prediction distribution

### Infrastructure
- Latency (p50, p95, p99)
- Error rate
- Throughput (predictions/second)
- Memory/CPU usage

### Business Metrics
- Click-through rate (recommendations)
- Conversion rate
- Revenue impact

---

## Retraining Strategy

| Trigger | Approach |
|---|---|
| **Scheduled** | Retrain weekly/monthly regardless | Simple but may waste resources |
| **Performance-based** | Retrain when monitored metric drops below threshold | Efficient but needs labeled data |
| **Drift-based** | Retrain when PSI > threshold | Works without labels |
| **Continuous** | Online learning — update model with each new data point | Complex, risk of instability |

---

## Interview Questions

1. How would you detect that a deployed model is degrading?
2. What's the difference between data drift and concept drift?
3. How do you monitor a model when you don't have immediate labels?
4. Design a retraining pipeline — when to trigger and how to validate?
]]>
