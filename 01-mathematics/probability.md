<![CDATA[# Probability for Machine Learning

> **Interview weight:** ⭐⭐⭐⭐ — Directly tested in ML theory rounds.  
> **Time to study:** 5–6 hours.  
> **Goal:** Be able to reason about uncertainty, apply Bayes' theorem, and explain probabilistic models.

---

## What Interviewers Actually Test

- "If a medical test has 99% sensitivity and the disease is rare (1%), what's the probability a positive test is correct?" (Bayes)
- "Explain the difference between generative and discriminative models" (joint vs conditional probability)
- "Why do we maximize log-likelihood instead of likelihood?"
- "Explain Naïve Bayes. What's the 'naïve' assumption?"

---

## Core Concepts

### 1. Probability Basics

```
P(A)           — Probability of event A
P(A ∩ B)       — Probability of A AND B
P(A ∪ B)       — Probability of A OR B = P(A) + P(B) - P(A ∩ B)
P(A | B)       — Probability of A GIVEN B = P(A ∩ B) / P(B)
```

**Independence:** A and B are independent if P(A ∩ B) = P(A) · P(B).

**Interview insight:** Naïve Bayes assumes all features are independent given the class label — that's the "naïve" part.

### 2. Bayes' Theorem

```
P(A | B) = P(B | A) · P(A) / P(B)
```

In ML terms:
```
P(class | features) = P(features | class) · P(class) / P(features)
  ↑ posterior          ↑ likelihood        ↑ prior    ↑ evidence
```

**Classic interview problem:**

> A disease affects 1 in 1000 people. A test has 99% sensitivity (true positive rate) and 1% false positive rate. You test positive. What's the probability you actually have the disease?

```python
# Bayes' theorem calculation
p_disease = 0.001           # Prior: P(D)
p_no_disease = 0.999        # P(¬D)
p_pos_given_disease = 0.99  # Sensitivity: P(+|D)
p_pos_given_no_disease = 0.01  # False positive rate: P(+|¬D)

# P(+) = P(+|D)·P(D) + P(+|¬D)·P(¬D)
p_positive = p_pos_given_disease * p_disease + p_pos_given_no_disease * p_no_disease
# = 0.99 * 0.001 + 0.01 * 0.999 = 0.01098

# P(D|+) = P(+|D)·P(D) / P(+)
p_disease_given_pos = (p_pos_given_disease * p_disease) / p_positive
# = 0.00099 / 0.01098 ≈ 0.09 → only 9%!
```

**The lesson:** Even with a 99% accurate test, a rare disease means most positive tests are false positives. This is why **class imbalance** matters in ML.

### 3. Common Distributions

| Distribution | Type | Parameters | ML Use |
|---|---|---|---|
| **Bernoulli** | Discrete | p (success probability) | Binary classification output |
| **Binomial** | Discrete | n, p | Number of successes in n trials |
| **Poisson** | Discrete | λ (rate) | Count data, rare events |
| **Gaussian (Normal)** | Continuous | μ, σ² | Everywhere — errors, features, priors |
| **Uniform** | Continuous | a, b | Random initialization, hyperparameter sampling |
| **Exponential** | Continuous | λ | Time between events |

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy import stats

# Generate and plot a Gaussian distribution
x = np.linspace(-4, 4, 100)
y = stats.norm.pdf(x, loc=0, scale=1)  # μ=0, σ=1
plt.plot(x, y)
plt.title("Standard Normal Distribution")
plt.xlabel("x")
plt.ylabel("Probability Density")
plt.show()
```

### 4. Expectation, Variance, and Covariance

```
E[X] = Σ xᵢ · P(xᵢ)                          — Expected (average) value
Var(X) = E[(X - E[X])²] = E[X²] - (E[X])²    — Spread of the distribution
Cov(X, Y) = E[(X - E[X])(Y - E[Y])]           — How two variables move together
```

**Interview insight:**
- **Bias of an estimator:** E[θ̂] - θ. An unbiased estimator has E[θ̂] = θ.
- **Variance of an estimator:** How much θ̂ fluctuates across different samples.
- Bias-variance tradeoff in ML models is built on this.

### 5. Maximum Likelihood Estimation (MLE)

Find the parameters θ that maximize the probability of observing the data:

```
θ_MLE = argmax_θ  P(data | θ)
      = argmax_θ  Π P(xᵢ | θ)         — for independent data
      = argmax_θ  Σ log P(xᵢ | θ)     — log-likelihood (numerically stable)
```

**Why log?** Products of small probabilities → underflow. Sums of logs are numerically stable.

**Example:** For logistic regression, MLE of the weights is equivalent to minimizing binary cross-entropy loss.

### 6. Maximum A Posteriori (MAP)

Like MLE, but includes a prior on the parameters:

```
θ_MAP = argmax_θ  P(θ | data) = argmax_θ  P(data | θ) · P(θ)
```

**Interview insight:** 
- **MLE** = no regularization
- **MAP with Gaussian prior** = L2 regularization (Ridge)
- **MAP with Laplacian prior** = L1 regularization (Lasso)

This is one of the most elegant connections in ML.

### 7. Conditional Independence

Variables X and Y are conditionally independent given Z if:
```
P(X, Y | Z) = P(X | Z) · P(Y | Z)
```

**ML relevance:** This is the core assumption of:
- Naïve Bayes classifiers
- Hidden Markov Models
- Bayesian Networks

---

## Common Interview Questions

1. **Q: Two coins — one fair, one double-headed. You pick one randomly and flip it 3 times, getting 3 heads. What's the probability you picked the fair coin?**
   > P(fair|HHH) = P(HHH|fair)·P(fair) / P(HHH)  
   > = (1/8 · 1/2) / (1/8 · 1/2 + 1 · 1/2) = (1/16) / (9/16) = 1/9

2. **Q: Explain the difference between MLE and MAP.**
   > MLE finds parameters that maximize the data likelihood. MAP adds a prior belief about parameters. MAP with a Gaussian prior is equivalent to L2 regularization.

3. **Q: Why do we use log-likelihood in ML optimization?**
   > Because the likelihood is a product of probabilities (very small numbers) — taking the log converts products to sums, which are numerically stable and easier to differentiate.

4. **Q: Explain generative vs discriminative models.**
   > Generative models (Naïve Bayes, GMM) learn P(X|Y) and P(Y), then use Bayes to get P(Y|X). Discriminative models (logistic regression, SVM) directly learn P(Y|X) or the decision boundary.

---

## Try It Yourself

1. Solve the "Monty Hall problem" using Bayes' theorem. Verify with a simulation (10,000 trials).
2. Implement MLE for the parameters of a Gaussian distribution from data samples.
3. Build a Naïve Bayes text classifier from scratch — compute priors and likelihoods manually.

---

## Resources

- 📺 [StatQuest — Probability fundamentals playlist](https://www.youtube.com/c/joshstarmer)
- 📖 [Think Bayes (free online book)](https://greenteapress.com/wp/think-bayes/)
- 📖 [Mathematics for Machine Learning — Chapter 6](https://mml-book.github.io/)
]]>
