<![CDATA[# Case Study: Recommendation System

> **Interview relevance:** Very common system design + ML question at product companies.

---

## Problem Statement

Build a recommendation engine for an e-commerce platform. Given user browsing history and purchase data, recommend products the user is likely to buy.

## Approach 1: Collaborative Filtering

**Idea:** Users who agreed in the past will agree in the future.

### User-Based CF
Find similar users → recommend what they bought.

### Item-Based CF
Find similar items to what the user already bought.

### Matrix Factorization
Decompose the user-item rating matrix: R ≈ U · Vᵀ

```python
# Using SVD for recommendations
from scipy.sparse.linalg import svds
import numpy as np

# R = user-item rating matrix (users × items)
U, sigma, Vt = svds(R, k=50)  # k = latent dimensions
sigma = np.diag(sigma)
predicted_ratings = U @ sigma @ Vt
```

## Approach 2: Content-Based Filtering

Use item features (category, price, description) to recommend similar items.

```python
from sklearn.metrics.pairwise import cosine_similarity

item_features = tfidf_vectorizer.fit_transform(item_descriptions)
similarity_matrix = cosine_similarity(item_features)
```

## Evaluation Metrics

| Metric | What It Measures |
|---|---|
| **Precision@K** | Of top-K recommendations, how many are relevant? |
| **Recall@K** | Of all relevant items, how many appear in top-K? |
| **NDCG** | Ranking quality — rewards relevant items appearing higher |
| **MAP** | Mean average precision across all users |
| **Hit Rate** | % of users who got at least one relevant recommendation |

## Production Considerations

- **Cold start:** New users/items have no history → use content-based or popularity-based fallback
- **Scalability:** Precompute recommendations offline (batch) for most users; real-time for active users
- **Diversity:** Don't recommend 10 variations of the same product
- **A/B testing:** Always measure business metrics (CTR, conversion) alongside ML metrics

---

## Interview Questions

1. How would you handle the cold-start problem?
2. Compare collaborative vs content-based filtering.
3. How would you evaluate a recommendation system in production?
4. How do you balance exploration (new items) vs exploitation (known good items)?
]]>
