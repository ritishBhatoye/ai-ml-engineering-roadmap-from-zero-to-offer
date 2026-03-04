<![CDATA[# 🗺️ Learning Roadmap — Beginner → Intermediate → Advanced

> This roadmap is designed for a BTech CSE student with 3–6 months of dedicated preparation time.  
> Every topic maps directly to what interviewers test.

---

## How to Read This Roadmap

- **Each phase** builds on the previous one — don't skip ahead.
- **Checkboxes** are for your own tracking — fork this repo and check them off.
- **"Interview Signal"** tells you how heavily this topic is tested.
- **"Time Investment"** is a realistic estimate, not a minimum.

---

## Phase 1: Foundations (Weeks 1–6)

**Goal:** Be comfortable with the math behind ML, write clean Python data code, and train your first models.

| # | Topic | Content | Interview Signal | Time |
|---|-------|---------|:---:|---|
| - [ ] | **Linear Algebra** | Vectors, dot products, matrix multiplication, eigenvalues, SVD | ⭐⭐⭐ | 4–5 hrs |
| - [ ] | **Probability** | Bayes' theorem, distributions (Gaussian, Bernoulli, Poisson), expectation, variance | ⭐⭐⭐⭐ | 5–6 hrs |
| - [ ] | **Statistics** | Descriptive stats, hypothesis testing, p-values, confidence intervals, A/B testing basics | ⭐⭐⭐ | 4–5 hrs |
| - [ ] | **Calculus** | Derivatives, chain rule, partial derivatives, gradient descent intuition | ⭐⭐ | 3–4 hrs |
| - [ ] | **NumPy & Pandas** | Array operations, broadcasting, DataFrames, groupby, merge, apply | ⭐⭐⭐⭐ | 6–8 hrs |
| - [ ] | **Matplotlib & Seaborn** | Histograms, scatter plots, heatmaps, pair plots | ⭐⭐ | 3–4 hrs |
| - [ ] | **Supervised Learning** | Linear regression, logistic regression, k-NN, decision trees | ⭐⭐⭐⭐⭐ | 8–10 hrs |
| - [ ] | **Evaluation Metrics** | Accuracy, precision, recall, F1, AUC-ROC, confusion matrix, RMSE, MAE | ⭐⭐⭐⭐⭐ | 4–5 hrs |

### Phase 1 Deliverable
> **Project 1:** Exploratory Data Analysis — clean a messy dataset, generate insights, visualize findings.  
> Push to GitHub with a proper README.

### What You Should Be Able to Do After Phase 1
- [ ] Explain gradient descent to a non-technical person
- [ ] Write a `pandas` pipeline to clean and transform raw CSV data
- [ ] Train a logistic regression classifier and evaluate it properly
- [ ] Explain precision vs recall tradeoff with a real example
- [ ] Solve basic probability interview questions (Bayes, conditional probability)

---

## Phase 2: Core ML Engineering (Weeks 7–14)

**Goal:** Master the full classical ML toolkit, understand feature engineering deeply, and write SQL for data extraction.

| # | Topic | Content | Interview Signal | Time |
|---|-------|---------|:---:|---|
| - [ ] | **Bias-Variance Tradeoff** | Underfitting vs overfitting, model complexity curves, generalization | ⭐⭐⭐⭐⭐ | 3–4 hrs |
| - [ ] | **Regularization** | L1 (Lasso), L2 (Ridge), elastic net, dropout, early stopping | ⭐⭐⭐⭐ | 4–5 hrs |
| - [ ] | **Feature Engineering** | Encoding (one-hot, target, ordinal), scaling, binning, interaction features, feature selection | ⭐⭐⭐⭐⭐ | 6–8 hrs |
| - [ ] | **Unsupervised Learning** | K-means, hierarchical clustering, PCA, t-SNE, DBSCAN | ⭐⭐⭐ | 5–6 hrs |
| - [ ] | **Ensemble Methods** | Bagging, boosting (AdaBoost, GBDT, XGBoost, LightGBM), random forests, stacking | ⭐⭐⭐⭐⭐ | 6–8 hrs |
| - [ ] | **Cross-Validation** | K-fold, stratified, time-series split, nested CV | ⭐⭐⭐⭐ | 3–4 hrs |
| - [ ] | **SQL for ML** | Joins, window functions, CTEs, subqueries, aggregation for feature tables | ⭐⭐⭐⭐ | 6–8 hrs |
| - [ ] | **Clean ML Code** | Modular scripts, type hints, config files, reproducibility, `sklearn` pipelines | ⭐⭐⭐ | 4–5 hrs |

### Phase 2 Deliverable
> **Project 2:** Supervised ML Pipeline — predict house prices or customer churn with full preprocessing, model selection, hyperparameter tuning, and evaluation.  
> Push to GitHub with model comparison results.

### What You Should Be Able to Do After Phase 2
- [ ] Explain why XGBoost outperforms vanilla decision trees
- [ ] Write a `sklearn` pipeline with preprocessing and model training
- [ ] Discuss feature engineering strategies for categorical vs numerical features
- [ ] Write SQL queries with window functions to build feature tables
- [ ] Explain L1 vs L2 regularization and when to use each

---

## Phase 3: Deep Learning + System Design (Weeks 15–20)

**Goal:** Understand modern deep learning architectures and how ML systems work in production.

| # | Topic | Content | Interview Signal | Time |
|---|-------|---------|:---:|---|
| - [ ] | **Neural Network Basics** | Perceptrons, backpropagation, activations (ReLU, sigmoid, softmax), loss functions | ⭐⭐⭐⭐ | 5–6 hrs |
| - [ ] | **CNNs** | Convolution, pooling, stride/padding, LeNet → ResNet intuition, transfer learning | ⭐⭐⭐⭐ | 6–8 hrs |
| - [ ] | **RNNs & LSTMs** | Sequence modeling, vanishing gradients, LSTM gates, bidirectional RNNs | ⭐⭐⭐ | 5–6 hrs |
| - [ ] | **Transformers** | Self-attention, positional encoding, encoder-decoder, BERT/GPT intuition | ⭐⭐⭐⭐ | 5–6 hrs |
| - [ ] | **ML Pipeline Design** | Data ingestion → feature store → training → serving → monitoring | ⭐⭐⭐⭐ | 5–6 hrs |
| - [ ] | **Data Leakage** | Types, detection, prevention strategies | ⭐⭐⭐⭐⭐ | 3–4 hrs |
| - [ ] | **Monitoring & Drift** | Data drift, concept drift, PSI, model performance decay, retraining triggers | ⭐⭐⭐ | 4–5 hrs |
| - [ ] | **Case Studies** | Recommendation system, spam classifier, credit risk model | ⭐⭐⭐⭐ | 8–10 hrs |

### Phase 3 Deliverable
> **Project 3:** Deep Learning Classifier — image classification on CIFAR-10 or a medical imaging dataset using PyTorch CNN. Include training curves, confusion matrix, and model comparison.

### What You Should Be Able to Do After Phase 3
- [ ] Draw and explain the architecture of a basic CNN
- [ ] Explain why transformers replaced RNNs for most NLP tasks
- [ ] Design an ML pipeline on a whiteboard (data → features → model → serving)
- [ ] Identify 3 types of data leakage in a given dataset
- [ ] Discuss how you would monitor a deployed model for drift

---

## Phase 4: Deployment + Interview Sprint (Weeks 21–24)

**Goal:** Deploy a model, polish your portfolio, and perform at interview level.

| # | Topic | Content | Interview Signal | Time |
|---|-------|---------|:---:|---|
| - [ ] | **Flask / FastAPI** | REST API endpoints, request/response handling, model loading, async basics | ⭐⭐⭐ | 5–6 hrs |
| - [ ] | **Docker** | Dockerfile, multi-stage builds, docker-compose, image optimization | ⭐⭐⭐ | 4–5 hrs |
| - [ ] | **Cloud Overview** | AWS SageMaker, GCP Vertex AI, S3/GCS, EC2/Compute Engine — conceptual | ⭐⭐ | 3–4 hrs |
| - [ ] | **ML Coding Questions** | Implement k-NN, logistic regression, K-means from scratch; numpy-based problems | ⭐⭐⭐⭐ | 8–10 hrs |
| - [ ] | **Mock Interviews** | Pair practice, timed system design, behavioral STAR stories | ⭐⭐⭐⭐⭐ | 6–8 hrs |
| - [ ] | **Resume & GitHub Polish** | 1-page resume, pinned repos, project READMEs, CI badges | ⭐⭐⭐⭐ | 4–5 hrs |

### Phase 4 Deliverable
> **Project 4:** End-to-End Deployed Model — train a spam classifier, wrap in FastAPI, containerize with Docker, add CI/CD via GitHub Actions, deploy to a cloud VM or serverless endpoint.

### What You Should Be Able to Do After Phase 4
- [ ] Build and run a Docker container for an ML API
- [ ] Implement logistic regression from scratch in NumPy
- [ ] Clearly articulate your project decisions in a mock interview
- [ ] Present a resume with quantified project impact
- [ ] Confidently discuss ML tradeoffs: latency vs throughput, precision vs recall, batch vs real-time

---

## Summary: The Progression

```
Week  1–6  │  "I can clean data and train a model"
Week  7–14 │  "I understand WHY models work and can engineer features"
Week 15–20 │  "I can discuss deep learning and design ML systems"
Week 21–24 │  "I can deploy models and ace interviews"
```

---

## How to Track Your Progress

1. **Fork this repository.**
2. Check off the boxes above as you complete each topic.
3. Push your projects to separate GitHub repos and link them in your resume.
4. Use the [`WEEKLY_PLAN.md`](WEEKLY_PLAN.md) for day-by-day structure.

---

> **Remember:** Interviewers don't test how many videos you watched.  
> They test whether you can *explain*, *build*, and *reason* about ML systems.
]]>
