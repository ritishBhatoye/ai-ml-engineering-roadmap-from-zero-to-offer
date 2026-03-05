# Complete Interview Preparation Guide

> This guide covers everything you need to ace ML engineer interviews — from theory to coding to system design.

---

## Table of Contents

1. [Interview Format](#1-interview-format)
2. [ML Theory Questions](#2-ml-theory-questions)
3. [Coding Questions](#3-coding-questions)
4. [SQL Questions](#4-sql-questions)
5. [System Design Questions](#5-system-design-questions)
6. [Behavioral Questions](#6-behavioral-questions)
7. [Evaluation Rubric](#7-evaluation-rubric)
8. [Mock Interview Plan](#8-mock-interview-plan)

---

## 1. Interview Format

### Typical ML Engineer Interview Pipeline

| Round | Type | Duration | What They Test |
|-------|------|----------|----------------|
| 1 | Screening (Phone/Video) | 30 min | Background, projects, basic ML |
| 2 | Coding Test (Online) | 45–60 min | Data structures, algorithms |
| 3 | ML Coding (Live) | 45 min | Implement ML algorithm from scratch |
| 4 | ML Theory | 45 min | Core concepts, tradeoffs |
| 5 | System Design | 45 min | ML pipeline design |
| 6 | Behavioral | 30 min | Team fit, past projects |

---

## 2. ML Theory Questions

### Must-Know Concepts

#### Bias-Variance Tradeoff
- **Q: Explain bias-variance tradeoff**
- **A:** High bias = underfitting (misses patterns). High variance = overfitting (memorizes noise). Goal: find sweet spot that generalizes.

#### Regularization
- **Q: Difference between L1 and L2?**
- **A:** L1 (Lasso) adds sum of absolute weights → sparse feature selection. L2 (Ridge) adds sum of squared weights → shrinks weights evenly.

#### Evaluation Metrics
- **Q: When to use F1 vs AUC?**
- **A:** F1 when classes are imbalanced and you care about precision/recall balance. AUC when you want to evaluate across all thresholds.

#### Data Leakage
- **Q: How to prevent data leakage?**
- **A:** Always split data BEFORE feature engineering. Use cross-validation properly. Never use future information.

### Practice Questions

```markdown
1. Explain how XGBoost differs from Random Forest
2. What is the kernel trick in SVM?
3. How does batch normalization help training?
4. Why do we use dropout in neural networks?
5. Explain the vanishing gradient problem
6. What is transfer learning and when to use it?
7. How do you handle class imbalance?
8. Explain cross-validation and why k=5 or k=10
9. What is feature importance and how do tree models compute it?
10. Difference between precision and recall?
```

---

## 3. Coding Questions

### Must-Implement From Scratch

| Algorithm | Time Limit | Hint |
|-----------|------------|------|
| Linear Regression | 20 min | Use gradient descent |
| Logistic Regression | 25 min | Use sigmoid + gradient descent |
| k-NN | 15 min | Use numpy for distance |
| K-Means | 25 min | Iterate assignment and update |
| Decision Tree | 30 min | Use information gain |

### Example: Implement Logistic Regression

```python
import numpy as np

def sigmoid(z):
    return 1 / (1 + np.exp(-z))

def fit(X, y, lr=0.01, epochs=1000):
    m, n = X.shape
    weights = np.zeros(n)
    bias = 0
    
    for _ in range(epochs):
        linear = np.dot(X, weights) + bias
        predictions = sigmoid(linear)
        
        dw = (1/m) * np.dot(X.T, (predictions - y))
        db = (1/m) * np.sum(predictions - y)
        
        weights -= lr * dw
        bias -= lr * db
    
    return weights, bias

def predict(X, weights, bias):
    linear = np.dot(X, weights) + bias
    return sigmoid(linear) > 0.5
```

### Practice Problems

```markdown
Easy:
- Implement softmax function
- Compute confusion matrix
- Calculate precision, recall, F1

Medium:
- Implement k-NN from scratch
- Implement decision tree (Gini impurity)
- Implement gradient descent for linear regression

Hard:
- Implement K-means clustering
- Build a simple neural network from scratch
- Implement backpropagation
```

---

## 4. SQL Questions

### Must-Know Concepts

- JOINs (INNER, LEFT, RIGHT, FULL)
- Window Functions (ROW_NUMBER, RANK, DENSE_RANK, LAG, LEAD)
- CTEs (Common Table Expressions)
- GROUP BY with aggregations
- Subqueries

### Practice Queries

```sql
-- Top 3 products by revenue per category
SELECT category, product, revenue
FROM (
    SELECT category, product, revenue,
           ROW_NUMBER() OVER (PARTITION BY category ORDER BY revenue DESC) as rn
    FROM products
) ranked
WHERE rn <= 3;

-- Month-over-month growth
SELECT 
    month,
    revenue,
    LAG(revenue) OVER (ORDER BY month) as prev_month,
    (revenue - LAG(revenue) OVER (ORDER BY month)) / LAG(revenue) OVER (ORDER BY month) as growth
FROM monthly_sales;

-- Build feature table for ML
SELECT 
    user_id,
    COUNT(*) as total_purchases,
    SUM(amount) as total_revenue,
    AVG(amount) as avg_order_value,
    MAX(created_at) as last_purchase,
    DATEDIFF(NOW(), MAX(created_at)) as days_since_last
FROM orders
GROUP BY user_id;
```

---

## 5. System Design Questions

### Common Problems

| Problem | What They Test |
|---------|---------------|
| Design a recommendation system | Understanding of collaborative filtering, content-based, tradeoffs |
| Design a spam classifier | End-to-end ML pipeline, data handling, deployment |
| Design a fraud detection system | Handling imbalanced data, real-time processing, latency |
| Design an ML pipeline for X | Data processing, feature store, model serving, monitoring |

### Framework for System Design

```
1. Clarify Requirements
   - What are we building?
   - What are the key metrics?
   - What are the constraints?

2. Data Pipeline
   - Data collection → ingestion → processing → features
   
3. Model Development
   - Training → validation → testing
   
4. Serving
   - Batch vs real-time
   - API design
   
5. Monitoring
   - Data drift, model drift
   - Performance metrics
   
6. Tradeoffs
   - Latency vs accuracy
   - Batch size, model complexity
```

---

## 6. Behavioral Questions

### STAR Method

| Component | What It Means |
|-----------|---------------|
| **S**ituation | Set the context |
| **T**ask | Describe your responsibility |
| **A**ction | Explain what you did |
| **R**esult | Share the outcome (quantify!) |

### Common Questions

```markdown
1. Tell me about yourself
2. Why do you want to be an ML engineer?
3. Describe a challenging ML project you worked on
4. How do you handle disagreements with teammates?
5. Tell me about a time you failed
6. How do you stay updated with ML?
7. Why our company?
8. Where do you see yourself in 5 years?
```

### Good STAR Example

> **Q: Tell me about a time you failed**
> 
> **S:** In my internship, I built a churn prediction model that achieved 95% accuracy.
> 
> **T:** I was asked to deploy it to production.
> 
> **A:** During deployment, I discovered severe data leakage — I was using future purchase data as features. I had to rebuild the model with proper feature engineering.
> 
> **R:** The corrected model achieved 78% accuracy but was actually deployable. I also created a checklist to prevent leakage in future projects.

---

## 7. Evaluation Rubric

### How Interviewers Score You

| Dimension | Weight | 5/5 | 3/5 | 1/5 |
|-----------|--------|-----|-----|-----|
| **Problem Solving** | 30% | Breaks problem down, considers edge cases | Solves but misses edge cases | Can't approach problem |
| **Technical Depth** | 25% | Deep understanding, knows tradeoffs | Surface understanding | Can't explain concepts |
| **Coding Quality** | 20% | Clean, modular, tested | Works but messy | Doesn't compile |
| **Communication** | 15% | Thinks out loud, clarifies | Explains what doing | Silent or rambling |
| **ML Intuition** | 10% | Aware of practical issues | Knows theory only | No awareness |

### Red Flags (Automatic Fail)

- Can't explain bias-variance
- Uses accuracy on imbalanced data
- Doesn't ask clarifying questions
- Can't justify model choice
- Ignores production concerns

---

## 8. Mock Interview Plan

### Phase 1: Self-Practice (Weeks 20–21)

| Activity | Time | Goal |
|----------|------|------|
| Record yourself answering 10 theory Qs | 3 hrs | Get comfortable speaking |
| Solve 10 ML coding problems with timer | 3 hrs | Build speed |
| Review your 4 projects | 2 hrs | Be ready to discuss |

### Phase 2: Peer Practice (Weeks 22–23)

| Session | Focus | Duration |
|---------|-------|----------|
| Mock 1 | ML Theory | 45 min |
| Mock 2 | ML Coding | 45 min |
| Mock 3 | System Design | 45 min |
| Mock 4 | Behavioral | 30 min |

### Phase 3: Real Interviews (Week 24+)

- Apply to 5–10 positions per week
- Treat real interviews as practice
- Ask for feedback

### Finding Mock Interview Partners

- **Pramp** — Free peer practice
- **Interviewing.io** — Free with real engineers
- **Friends** — Ask classmates
- **Discord** — Join ML interview prep servers

---

## Resources

| Resource | Link |
|----------|------|
| LeetCode | leetcode.com |
| HackerRank SQL | hackerrank.com/domains/sql |
| Pramp | pramp.com |
| Interviewing.io | interviewing.io |
| This repo's coding questions | `06-ml-coding/coding-questions.md` |

---

## Final Tips

1. **Start interviewing early** — Don't wait until you're "ready"
2. **Learn from every interview** — Ask for feedback
3. **Focus on fundamentals** — New models come and go, fundamentals stay
4. **Practice out loud** — Recording yourself helps
5. **Stay confident** — You've done the work

---

> **Good luck! You've got this.**
