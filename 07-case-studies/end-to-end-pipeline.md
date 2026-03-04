<![CDATA[# Case Study: End-to-End ML Pipeline

> **Interview relevance:** Tests your understanding of the full ML lifecycle beyond model training.

---

## The Full Pipeline

```
Raw Data → Ingestion → Validation → Feature Engineering → Training → 
Evaluation → Model Registry → Deployment → Monitoring → Retraining
```

### Step 1: Data Ingestion
- Source: database, API, file storage (S3/GCS)
- Format: structured (CSV, Parquet) or unstructured (images, text)
- Frequency: batch (daily/weekly) or streaming (real-time)

### Step 2: Data Validation
```python
import great_expectations as ge

df_ge = ge.from_pandas(df)
df_ge.expect_column_values_to_not_be_null("user_id")
df_ge.expect_column_values_to_be_between("age", 0, 120)
df_ge.expect_column_values_to_be_in_set("status", ["active", "churned"])
```

### Step 3: Feature Engineering
- Build a reproducible feature pipeline (sklearn Pipeline or custom)
- Store features in a feature store for reuse across models

### Step 4: Training
- Experiment tracking with MLflow or Weights & Biases
- Hyperparameter tuning with cross-validation
- Log: parameters, metrics, artifacts, dataset version

### Step 5: Evaluation
- Compare against baseline and previous production model
- Check for bias and fairness
- Validate on a held-out test set AND on recent data

### Step 6: Model Registry
- Version the model, link to training data and code
- Staging → Production promotion workflow

### Step 7: Deployment
- REST API (FastAPI) wrapped in Docker container
- CI/CD pipeline: test → build → deploy
- Canary deployment: route 5% of traffic to new model

### Step 8: Monitoring
- Track prediction distribution shifts (PSI)
- Monitor latency, error rates, throughput
- Set alerts for model performance degradation

### Step 9: Retraining
- Trigger: performance decay, data drift, or scheduled
- Automated pipeline: retrain → validate → deploy (if passes)

---

## Interview Questions

1. Walk me through deploying a model from training to serving real traffic.
2. How would you detect that a model needs retraining?
3. What's the difference between batch and real-time inference?
4. How do you prevent data leakage in a production pipeline?
]]>
