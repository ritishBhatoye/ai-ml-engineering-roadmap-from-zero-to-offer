<![CDATA[# Statistics for Machine Learning

> **Interview weight:** ⭐⭐⭐ — Tested in data science–flavored ML roles and A/B testing discussions.  
> **Time to study:** 4–5 hours.  
> **Goal:** Understand descriptive statistics, hypothesis testing, and how statistics informs ML decisions.

---

## What Interviewers Actually Test

- "How would you determine if Model A is significantly better than Model B?" (hypothesis testing)
- "Explain p-value in plain English"
- "How do you detect and handle outliers?"
- "Walk me through how you'd set up an A/B test for a new recommendation model"

---

## Core Concepts

### 1. Descriptive Statistics

```python
import numpy as np

data = np.array([12, 15, 18, 22, 25, 28, 30, 35, 40, 120])

mean   = np.mean(data)      # 34.5 — sensitive to outliers
median = np.median(data)    # 26.5 — robust to outliers
std    = np.std(data)       # 29.55
q1     = np.percentile(data, 25)   # 17.25
q3     = np.percentile(data, 75)   # 33.75
iqr    = q3 - q1                   # 16.5
```

**Interview insight:** Always prefer **median** and **IQR** over **mean** and **std** when data has outliers (e.g., income data, click counts).

### 2. Correlation vs Causation

```python
import numpy as np

# Pearson correlation — measures linear relationship
from scipy.stats import pearsonr
r, p_value = pearsonr(x, y)  # r ∈ [-1, 1]

# Spearman correlation — measures monotonic relationship (rank-based)
from scipy.stats import spearmanr
rho, p_value = spearmanr(x, y)
```

| Metric | Measures | When to Use |
|--------|----------|-------------|
| **Pearson** | Linear relationship | Both variables are continuous and roughly normal |
| **Spearman** | Monotonic relationship | Ordinal data or non-linear monotonic relationships |

> **Correlation ≠ Causation.** Ice cream sales and drowning deaths are correlated (both increase in summer), but one doesn't cause the other.

### 3. Hypothesis Testing

**The framework:**
1. **Null hypothesis (H₀):** "There is no effect / no difference."
2. **Alternative hypothesis (H₁):** "There IS an effect / difference."
3. **Compute a test statistic** from the data.
4. **Calculate the p-value:** probability of seeing this result (or more extreme) if H₀ is true.
5. **Compare p-value to significance level α** (typically 0.05).
   - p < α → reject H₀ (result is statistically significant)
   - p ≥ α → fail to reject H₀

```python
from scipy import stats

# Example: Is Model A's accuracy significantly different from Model B's?
accuracy_a = [0.85, 0.87, 0.86, 0.88, 0.84, 0.86, 0.87, 0.85, 0.86, 0.88]
accuracy_b = [0.82, 0.83, 0.84, 0.81, 0.83, 0.82, 0.84, 0.83, 0.82, 0.83]

# Paired t-test (same test sets, different models)
t_stat, p_value = stats.ttest_rel(accuracy_a, accuracy_b)
print(f"t-statistic: {t_stat:.4f}, p-value: {p_value:.4f}")
# If p_value < 0.05 → Model A is significantly better
```

### 4. Common Statistical Tests

| Test | When to Use | Example |
|------|-------------|---------|
| **t-test (1-sample)** | Is the mean different from a known value? | "Is our model's precision different from 0.90?" |
| **t-test (2-sample)** | Are two group means different? | "Do users in Group A click more than Group B?" |
| **Paired t-test** | Are two paired measurements different? | "Model A vs Model B on the SAME test sets" |
| **Chi-squared test** | Are two categorical variables independent? | "Is churn related to plan type?" |
| **ANOVA** | Are 3+ group means different? | "Compare 3 models' performance" |

### 5. Confidence Intervals

A 95% confidence interval means: "If we repeated this experiment 100 times, ~95 of the intervals would contain the true parameter."

```python
import numpy as np
from scipy import stats

data = [0.85, 0.87, 0.86, 0.88, 0.84]
mean = np.mean(data)
se = stats.sem(data)  # Standard error of the mean
ci = stats.t.interval(0.95, df=len(data)-1, loc=mean, scale=se)
print(f"95% CI: ({ci[0]:.4f}, {ci[1]:.4f})")
```

**Interview insight:** When reporting model performance, always report confidence intervals, not just point estimates. "Our model achieves 87.2% accuracy (95% CI: 85.1%–89.3%)" is much more rigorous.

### 6. A/B Testing for ML

**Step-by-step framework:**

1. **Define the metric** — CTR, conversion rate, revenue per user.
2. **State hypotheses:**
   - H₀: New model performs the same as the old model
   - H₁: New model performs better
3. **Calculate sample size:**
   ```python
   from statsmodels.stats.power import TTestIndPower
   
   effect_size = 0.2   # Expected improvement (Cohen's d)
   alpha = 0.05        # Significance level
   power = 0.8         # Probability of detecting a true effect
   
   analysis = TTestIndPower()
   n = analysis.solve_power(effect_size=effect_size, alpha=alpha, power=power)
   print(f"Required sample size per group: {int(n)}")  # ~394
   ```
4. **Run the experiment** — randomly assign users (50/50 split).
5. **Analyse results** — use a t-test or z-test depending on sample size.
6. **Make a decision** — consider practical significance, not just statistical significance.

### 7. Handling Outliers

| Method | Approach | When to Use |
|--------|----------|-------------|
| **IQR method** | Remove points < Q1 - 1.5·IQR or > Q3 + 1.5·IQR | General-purpose |
| **Z-score** | Remove points with \|z\| > 3 | When data is approximately normal |
| **Winsorization** | Cap extreme values at a percentile (e.g., 1st and 99th) | When you don't want to lose data |
| **Robust models** | Use models resistant to outliers (e.g., median regression, tree-based models) | When outliers are informative |

---

## Common Interview Questions

1. **Q: Explain p-value in plain English.**
   > A p-value is the probability of observing data this extreme (or more) if the null hypothesis were true. It is NOT the probability that the hypothesis is true.

2. **Q: What's the difference between Type I and Type II errors?**
   > Type I (false positive): rejecting H₀ when it's actually true. Type II (false negative): failing to reject H₀ when it's actually false. There's a tradeoff — reducing one increases the other.

3. **Q: How would you design an A/B test for a new ranking model?**
   > Define the primary metric (e.g., CTR), calculate required sample size for desired power, randomize users into control/treatment, run for sufficient time (account for seasonality), analyze with a statistical test, check for practical significance.

4. **Q: When should you use non-parametric tests?**
   > When the data doesn't follow a normal distribution, sample sizes are small, or the data is ordinal. Examples: Mann-Whitney U test, Wilcoxon signed-rank test.

---

## Try It Yourself

1. Generate two sets of model accuracy scores. Perform a paired t-test. Interpret the result.
2. Build an outlier detection pipeline: try IQR, Z-score, and Isolation Forest on a dataset with known outliers.
3. Design an A/B test for a new recommendation algorithm: write out the full plan (metric, hypotheses, sample size, duration, analysis).

---

## Resources

- 📺 [StatQuest — Hypothesis testing playlist](https://www.youtube.com/c/joshstarmer)
- 📖 [Practical Statistics for Data Scientists (O'Reilly)](https://www.oreilly.com/library/view/practical-statistics-for/9781492072935/)
- 📖 [Think Stats (free online book)](https://greenteapress.com/thinkstats2/)
]]>
