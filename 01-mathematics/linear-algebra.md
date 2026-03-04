<![CDATA[# Linear Algebra for Machine Learning

> **Interview weight:** ⭐⭐⭐ — Tested indirectly through model understanding.  
> **Time to study:** 4–5 hours.  
> **Goal:** Understand the math behind PCA, SVD, gradient descent, and neural networks.

---

## What Interviewers Actually Test

They won't ask you to invert a 5×5 matrix by hand. They **will** ask:

- "How does PCA work?" (requires understanding eigenvalues/eigenvectors)
- "What happens during matrix factorization in recommendation systems?"
- "Why do we multiply weights by inputs in a neural network?" (linear transformation)
- "Explain SVD and where it's used in ML"

---

## Core Concepts (Only What You Need)

### 1. Vectors

A vector is an ordered list of numbers. In ML, a vector is a **data point** or a **feature set**.

```python
import numpy as np

# A data point with 3 features
x = np.array([1.5, 2.3, 0.7])

# Vector operations you must know:
# Dot product — measures similarity
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
dot = np.dot(a, b)  # 1*4 + 2*5 + 3*6 = 32

# Norm — measures magnitude (distance from origin)
norm = np.linalg.norm(a)  # sqrt(1² + 2² + 3²) = 3.74

# Cosine similarity — dot product normalized by magnitudes
cos_sim = np.dot(a, b) / (np.linalg.norm(a) * np.linalg.norm(b))
```

**Interview insight:** Cosine similarity is used in recommendation systems, NLP (word embeddings), and information retrieval. Know how to compute it.

### 2. Matrices

A matrix is a 2D array of numbers. In ML:
- **Data matrix** X: rows = samples, columns = features
- **Weight matrix** W: transforms inputs in neural networks
- **Covariance matrix**: captures feature correlations

```python
# Data matrix: 3 samples, 4 features
X = np.array([
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12]
])

# Matrix multiplication — THE core operation in ML
W = np.random.randn(4, 2)  # Weight matrix: 4 inputs → 2 outputs
output = X @ W               # Shape: (3, 2)

# Transpose — swaps rows and columns
X_T = X.T  # Shape: (4, 3)
```

**Interview insight:** When someone asks "how does a layer in a neural network work?" — the answer is matrix multiplication followed by a non-linear activation.

### 3. Eigenvalues & Eigenvectors

- **Eigenvector:** A direction that doesn't change when a linear transformation is applied.
- **Eigenvalue:** How much the eigenvector is scaled.

```
A · v = λ · v
```

Where `A` is a matrix, `v` is the eigenvector, `λ` is the eigenvalue.

**Where this matters in ML:**
- **PCA:** Eigenvectors of the covariance matrix = principal components. Eigenvalues = variance explained.
- **Google's PageRank:** Eigenvector of the web link matrix.

```python
# PCA from scratch (simplified)
from numpy.linalg import eig

X_centered = X - X.mean(axis=0)
cov_matrix = np.cov(X_centered, rowvar=False)
eigenvalues, eigenvectors = eig(cov_matrix)

# Sort by eigenvalue (highest variance first)
idx = eigenvalues.argsort()[::-1]
eigenvalues = eigenvalues[idx]
eigenvectors = eigenvectors[:, idx]

# Project onto top 2 components
X_pca = X_centered @ eigenvectors[:, :2]
```

### 4. Singular Value Decomposition (SVD)

SVD decomposes any matrix into three matrices: `A = U · Σ · Vᵀ`

- **U:** Left singular vectors (row space)
- **Σ:** Diagonal matrix of singular values (importance)
- **Vᵀ:** Right singular vectors (column space)

**Where this matters in ML:**
- **Dimensionality reduction** (alternative to PCA)
- **Matrix factorization** in recommendation systems
- **Latent semantic analysis** in NLP

```python
U, S, Vt = np.linalg.svd(X, full_matrices=False)

# Low-rank approximation (keep top k singular values)
k = 2
X_approx = U[:, :k] @ np.diag(S[:k]) @ Vt[:k, :]
```

### 5. Matrix Properties You Should Know

| Property | What It Means | ML Relevance |
|----------|--------------|--------------|
| **Rank** | Number of linearly independent rows/columns | If rank < features → multicollinearity |
| **Determinant** | Scalar measure of "volume change" | Det ≈ 0 → matrix is singular (can't invert) |
| **Inverse** | A⁻¹ such that A·A⁻¹ = I | Used in closed-form linear regression: `w = (XᵀX)⁻¹Xᵀy` |
| **Positive definite** | All eigenvalues > 0 | Covariance matrices are always positive semi-definite |
| **Orthogonal** | Columns are unit vectors and mutually perpendicular | PCA eigenvectors are orthogonal |

---

## Common Interview Questions

1. **Q: Explain PCA. How do you choose the number of components?**
   > PCA finds the directions of maximum variance in the data. Each principal component is an eigenvector of the covariance matrix. Choose components by keeping enough to explain 90-95% of cumulative variance (scree plot).

2. **Q: What is the rank of a matrix and why does it matter?**
   > Rank = number of linearly independent columns. If a feature matrix has rank < number of features, some features are redundant (multicollinearity). This causes issues for models like linear regression.

3. **Q: Explain how matrix factorization works for recommendations.**
   > Decompose the user-item rating matrix R into two low-rank matrices: R ≈ U · Vᵀ. U captures user preferences, V captures item attributes. Missing entries in R can be predicted by dot products of latent vectors.

4. **Q: Why is the covariance matrix important in ML?**
   > It captures how features vary together. Diagonal = variance of each feature. Off-diagonal = covariance between features. PCA, Gaussian distributions, and Mahalanobis distance all depend on it.

---

## Try It Yourself

1. Implement cosine similarity between two text documents (represent as word count vectors).
2. Compute the covariance matrix of a 3-feature dataset and extract principal components manually.
3. Use SVD to compress an image (load as matrix, keep top-k singular values, reconstruct).

---

## Resources

- 📺 [3Blue1Brown — Essence of Linear Algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab) (must-watch)
- 📖 [Mathematics for Machine Learning — Chapter 2](https://mml-book.github.io/) (free PDF)
- 💻 [NumPy Linear Algebra docs](https://numpy.org/doc/stable/reference/routines.linalg.html)
]]>
