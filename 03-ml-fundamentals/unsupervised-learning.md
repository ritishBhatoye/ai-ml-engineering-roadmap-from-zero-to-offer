<![CDATA[# Unsupervised Learning

> **Interview weight:** ⭐⭐⭐ — Tested conceptually; less code-heavy than supervised learning.  
> **Time to study:** 5–6 hours.  
> **Goal:** Understand clustering, dimensionality reduction, and when to use each.

---

## 1. K-Means Clustering

**Idea:** Partition n data points into k clusters by minimizing within-cluster variance.

**Algorithm:**
1. Initialize k centroids randomly.
2. Assign each point to the nearest centroid.
3. Recompute centroids as the mean of assigned points.
4. Repeat steps 2–3 until convergence.

```python
import numpy as np

class KMeansScratch:
    def __init__(self, k=3, max_iters=100):
        self.k = k
        self.max_iters = max_iters
    
    def fit(self, X):
        # Random initialization
        idx = np.random.choice(len(X), self.k, replace=False)
        self.centroids = X[idx]
        
        for _ in range(self.max_iters):
            # Assign clusters
            distances = np.linalg.norm(X[:, np.newaxis] - self.centroids, axis=2)
            self.labels = np.argmin(distances, axis=1)
            
            # Update centroids
            new_centroids = np.array([X[self.labels == i].mean(axis=0) for i in range(self.k)])
            
            if np.allclose(self.centroids, new_centroids):
                break
            self.centroids = new_centroids
        
        return self
```

**Choosing k:** Use the **elbow method** (plot inertia vs k) or **silhouette score**.

**Interview Q: What are the limitations of K-means?**
> (1) Assumes spherical clusters of equal size. (2) Sensitive to initialization (use K-means++). (3) Must specify k in advance. (4) Doesn't handle non-convex shapes — use DBSCAN instead.

---

## 2. DBSCAN

**Idea:** Density-based clustering. Groups points that are closely packed, marks outliers.

- **ε (eps):** Radius of neighborhood.
- **min_samples:** Minimum points to form a dense region.

```python
from sklearn.cluster import DBSCAN

model = DBSCAN(eps=0.5, min_samples=5)
labels = model.fit_predict(X)
# labels == -1 → noise/outlier
```

**When to use over K-means:** Non-convex clusters, unknown k, need outlier detection.

---

## 3. Principal Component Analysis (PCA)

**Idea:** Find orthogonal directions (principal components) that capture maximum variance. Project data onto top-k components for dimensionality reduction.

**Steps:**
1. Center the data (subtract mean).
2. Compute covariance matrix.
3. Compute eigenvalues and eigenvectors.
4. Sort by eigenvalue (descending).
5. Project data onto top-k eigenvectors.

```python
from sklearn.decomposition import PCA
import matplotlib.pyplot as plt

# Reduce to 2 dimensions for visualization
pca = PCA(n_components=2)
X_pca = pca.fit_transform(X)

# How much variance is explained?
print(f"Explained variance: {pca.explained_variance_ratio_}")
# e.g., [0.72, 0.15] → first 2 components explain 87% of variance

# Scree plot — choosing number of components
pca_full = PCA().fit(X)
plt.plot(range(1, len(pca_full.explained_variance_ratio_) + 1),
         np.cumsum(pca_full.explained_variance_ratio_))
plt.axhline(y=0.95, color='r', linestyle='--', label="95% variance")
plt.xlabel("Number of Components")
plt.ylabel("Cumulative Explained Variance")
plt.legend()
plt.show()
```

**Interview Q: When should you use PCA?**
> (1) When you have many correlated features (reduce multicollinearity). (2) Before k-NN or SVM (curse of dimensionality). (3) For data visualization (project to 2D/3D). (4) To speed up training on high-dimensional data.

**Interview Q: What's the difference between PCA and t-SNE?**
> PCA is a linear method that preserves global structure (variance). t-SNE is non-linear and preserves local structure (neighbor relationships). Use PCA for preprocessing, t-SNE for visualization only (not meaningful for actual feature reduction).

---

## 4. Anomaly Detection

| Method | Approach | Best For |
|---|---|---|
| **Isolation Forest** | Randomly partition data; anomalies are isolated faster | High-dimensional data |
| **One-Class SVM** | Learn a boundary around normal data | When you have only "normal" samples |
| **DBSCAN** | Points labeled as noise = anomalies | Spatial/clustered data |
| **Z-score / IQR** | Statistical thresholds | Simple univariate detection |

```python
from sklearn.ensemble import IsolationForest

model = IsolationForest(contamination=0.05, random_state=42)
predictions = model.fit_predict(X)
# predictions == -1 → anomaly
```

---

## Common Interview Questions

1. **Q: How does PCA relate to SVD?**
   > PCA on centered data X is equivalent to performing SVD: X = UΣVᵀ. The right singular vectors V are the principal components. The singular values in Σ relate to the eigenvalues of the covariance matrix.

2. **Q: How would you evaluate clustering quality without labels?**
   > **Silhouette score:** Measures how similar a point is to its own cluster vs nearest cluster (-1 to 1, higher is better). **Inertia:** Within-cluster sum of squares (lower is better, but always decreases with more clusters). **Visual inspection** for 2D/3D data.

3. **Q: Explain the curse of dimensionality.**
   > As dimensions increase: (1) Data becomes sparse — need exponentially more data to maintain density. (2) Distances become less meaningful — all pairwise distances converge. (3) Algorithms like k-NN and k-Means degrade. Solution: dimensionality reduction (PCA) or feature selection.

---

## Try It Yourself

1. Implement K-means from scratch. Test on the Iris dataset. Compare with sklearn's version.
2. Apply PCA to a 20-feature dataset. Plot the scree plot and choose the number of components for 95% variance.
3. Use DBSCAN on a dataset with non-convex clusters. Compare results with K-means.

---

## Resources

- 📺 [StatQuest — PCA, Clustering](https://www.youtube.com/c/joshstarmer)
- 📖 [Hands-On ML — Chapter 8 (Dimensionality Reduction)](https://github.com/ageron/handson-ml2)
- 📖 [Hands-On ML — Chapter 9 (Unsupervised Learning)](https://github.com/ageron/handson-ml2)
]]>
