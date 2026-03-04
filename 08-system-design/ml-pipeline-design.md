<![CDATA[# ML Pipeline Design — System Design for Interns

> **Interview weight:** ⭐⭐⭐⭐ — Even interns are tested on high-level pipeline thinking.

---

## The Framework (Use This in Every Interview)

### Step 1: Clarify the Problem
- What is the business goal?
- What does success look like? (metric)
- Batch or real-time predictions?
- Scale: thousands or millions of predictions/day?

### Step 2: Data
- What data is available?
- How fresh does it need to be?
- Any labels? How are they collected?
- Data quality concerns?

### Step 3: Feature Engineering
- What features can we extract?
- Need a feature store?
- Online vs offline features?

### Step 4: Model Selection
- Start simple (logistic regression baseline)
- Justify complexity increase
- Training infrastructure: single machine or distributed?

### Step 5: Serving
- **Batch:** Precompute predictions on schedule → store in DB → serve via lookup
- **Real-time:** Model served via API → compute prediction on request

| Factor | Batch | Real-time |
|---|---|---|
| Latency | Minutes to hours | < 100ms |
| Freshness | Stale (last batch) | Live |
| Infra cost | Lower | Higher |
| Use case | Recommendations, reports | Fraud detection, search ranking |

### Step 6: Monitoring
- Input data distribution
- Prediction distribution
- Business metrics (CTR, conversion)
- Latency and error rates

### Step 7: Feedback Loop
- How do we collect labels?
- How often do we retrain?
- Automated vs manual retraining?

---

## Example: Design a Fraud Detection System

1. **Goal:** Flag fraudulent transactions in real-time
2. **Data:** Transaction history, user profile, device info, merchant data
3. **Features:** Transaction amount, time since last transaction, geo-location anomaly, device fingerprint
4. **Model:** Gradient boosted trees (fast inference) with real-time feature computation
5. **Serving:** Real-time API, < 50ms latency requirement
6. **Monitoring:** Track false positive rate daily, alert if > 2%
7. **Feedback:** Chargebacks provide labels (delayed by 30-60 days)

---

## Key Vocabulary

| Term | Definition |
|---|---|
| **Feature Store** | Centralized storage for computed features, shared across models |
| **Model Registry** | Versioned storage for trained models with metadata |
| **Shadow Mode** | New model runs alongside production model but doesn't serve; compare results |
| **Canary Deployment** | Route small % of traffic to new model, monitor, then scale up |
| **A/B Test** | Split traffic between old and new model, measure business metric |
]]>
