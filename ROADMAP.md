# Learning Roadmap — Beginner to Interview-Ready

> This roadmap is designed for a student with 3–6 months of dedicated preparation.
> Every topic maps directly to what interviewers test in ML internships and entry-level roles.

---

## How to Read This Roadmap

- **Each phase** builds on the previous — don't skip ahead
- **Checkboxes** are for your own tracking — fork this repo and check them off
- **"Interview Signal"** tells you how heavily this topic is tested (1-5 stars)
- **"Time Investment"** is a realistic estimate including practice

---

## Phase 1: Foundations (Weeks 1–6)

**Goal:** Master the math behind ML, write production-quality Python data code, and train your first models with proper evaluation.

### Topics

| # | Topic | Key Concepts | Interview Signal | Time |
|---|-------|-------------|:---:|:---:|
| 1.1 | **Linear Algebra** | Vectors, dot products, matrices, eigenvalues, SVD | ⭐⭐⭐ | 4–5 hrs |
| 1.2 | **Probability** | Bayes' theorem, distributions (Gaussian, Bernoulli, Poisson), expectation, variance | ⭐⭐⭐⭐ | 5–6 hrs |
| 1.3 | **Statistics** | Descriptive stats, hypothesis testing, p-values, confidence intervals, A/B testing | ⭐⭐⭐ | 4–5 hrs |
| 1.4 | **Calculus** | Derivatives, chain rule, partial derivatives, gradient descent intuition | ⭐⭐ | 3–4 hrs |
| 1.5 | **NumPy & Pandas** | Array operations, broadcasting, DataFrames, groupby, merge, apply | ⭐⭐⭐⭐ | 6–8 hrs |
| 1.6 | **Matplotlib & Seaborn** | Histograms, scatter plots, heatmaps, pair plots | ⭐⭐ | 3–4 hrs |
| 1.7 | **Supervised Learning Basics** | Linear regression, logistic regression, k-NN | ⭐⭐⭐⭐⭐ | 8–10 hrs |
| 1.8 | **Evaluation Metrics** | Accuracy, precision, recall, F1, AUC-ROC, confusion matrix, RMSE, MAE | ⭐⭐⭐⭐⭐ | 4–5 hrs |

### Phase 1 Deliverable

> **[Project 1: Exploratory Data Analysis](projects/01-eda-and-visualization/)**
> 
> Clean a messy dataset, generate insights, create visualizations.
> 
> **Why this matters:** Data cleaning and EDA are 80% of real ML work.

### After Phase 1, You Can:

- [ ] Explain gradient descent to a non-technical person
- [ ] Write a `pandas` pipeline to clean and transform raw CSV data
- [ ] Train a logistic regression classifier and evaluate it properly
- [ ] Explain precision vs recall tradeoff with a real example (e.g., fraud detection)
- [ ] Solve basic probability interview questions (Bayes, conditional probability)

---

## Phase 2: Core ML Engineering (Weeks 7–14)

**Goal:** Master the full classical ML toolkit, understand feature engineering deeply, and write SQL for data extraction.

### Topics

| # | Topic | Key Concepts | Interview Signal | Time |
|---|-------|-------------|:---:|:---:|
| 2.1 | **Bias-Variance Tradeoff** | Underfitting vs overfitting, model complexity curves, generalization | ⭐⭐⭐⭐⭐ | 3–4 hrs |
| 2.2 | **Regularization** | L1 (Lasso), L2 (Ridge), elastic net, dropout | ⭐⭐⭐⭐ | 4–5 hrs |
| 2.3 | **Feature Engineering** | Encoding, scaling, binning, interaction features, feature selection | ⭐⭐⭐⭐⭐ | 6–8 hrs |
| 2.4 | **Unsupervised Learning** | K-means, hierarchical clustering, PCA, t-SNE, DBSCAN | ⭐⭐⭐ | 5–6 hrs |
| 2.5 | **Ensemble Methods** | Bagging, boosting (AdaBoost, GBDT, XGBoost, LightGBM), stacking | ⭐⭐⭐⭐⭐ | 6–8 hrs |
| 2.6 | **Cross-Validation** | K-fold, stratified, time-series split, nested CV | ⭐⭐⭐⭐ | 3–4 hrs |
| 2.7 | **SQL for ML** | Joins, window functions, CTEs, subqueries, aggregation | ⭐⭐⭐⭐ | 6–8 hrs |
| 2.8 | **Clean ML Code** | Modular scripts, type hints, config files, reproducibility, sklearn pipelines | ⭐⭐⭐ | 4–5 hrs |

### Phase 2 Deliverable

> **[Project 2: Supervised ML Pipeline](projects/02-supervised-ml-pipeline/)**
> 
> Predict house prices or customer churn with full preprocessing, model selection, hyperparameter tuning, and evaluation.
> 
> **Why this matters:** This is what interviewers expect you to build in 45 minutes.

### After Phase 2, You Can:

- [ ] Explain why XGBoost typically outperforms vanilla decision trees
- [ ] Write a `sklearn` pipeline with preprocessing and model training
- [ ] Discuss feature engineering strategies for categorical vs numerical features
- [ ] Write SQL queries with window functions to build feature tables
- [ ] Explain L1 vs L2 regularization and when to use each

---

## Phase 3: Deep Learning + System Design (Weeks 15–20)

**Goal:** Understand modern deep learning architectures and how ML systems work in production.

### Topics

| # | Topic | Key Concepts | Interview Signal | Time |
|---|-------|-------------|:---:|:---:|
| 3.1 | **Neural Network Basics** | Perceptrons, backpropagation, activations (ReLU, sigmoid, softmax) | ⭐⭐⭐⭐ | 5–6 hrs |
| 3.2 | **CNNs** | Convolution, pooling, LeNet → ResNet intuition, transfer learning | ⭐⭐⭐⭐ | 6–8 hrs |
| 3.3 | **RNNs & LSTMs** | Sequence modeling, vanishing gradients, LSTM gates | ⭐⭐⭐ | 5–6 hrs |
| 3.4 | **Transformers** | Self-attention, positional encoding, BERT/GPT intuition | ⭐⭐⭐⭐ | 5–6 hrs |
| 3.5 | **ML Pipeline Design** | Data ingestion → feature store → training → serving → monitoring | ⭐⭐⭐⭐ | 5–6 hrs |
| 3.6 | **Data Leakage** | Types, detection, prevention strategies | ⭐⭐⭐⭐⭐ | 3–4 hrs |
| 3.7 | **Monitoring & Drift** | Data drift, concept drift, PSI, retraining triggers | ⭐⭐⭐ | 4–5 hrs |
| 3.8 | **Case Studies** | Recommendation system, spam classifier, credit risk model | ⭐⭐⭐⭐ | 8–10 hrs |

### Phase 3 Deliverable

> **[Project 3: Deep Learning Classifier](projects/03-deep-learning-classifier/)**
> 
> Image classification on CIFAR-10 or medical imaging using PyTorch CNN.
> 
> **Why this matters:** Shows you can train neural networks, tune hyperparameters, and interpret results.

### After Phase 3, You Can:

- [ ] Draw and explain the architecture of a basic CNN
- [ ] Explain why transformers replaced RNNs for most NLP tasks
- [ ] Design an ML pipeline on a whiteboard (data → features → model → serving)
- [ ] Identify 3 types of data leakage in a given dataset
- [ ] Discuss how you would monitor a deployed model for drift

---

## Phase 4: Deployment + Interview Sprint (Weeks 21–24)

**Goal:** Deploy a model, polish your portfolio, and perform at interview level.

### Topics

| # | Topic | Key Concepts | Interview Signal | Time |
|---|-------|-------------|:---:|:---:|
| 4.1 | **Flask / FastAPI** | REST API endpoints, request/response handling, async basics | ⭐⭐⭐ | 5–6 hrs |
| 4.2 | **Docker** | Dockerfile, multi-stage builds, docker-compose | ⭐⭐⭐ | 4–5 hrs |
| 4.3 | **Cloud Overview** | AWS SageMaker, GCP Vertex AI, S3, EC2 (conceptual) | ⭐⭐ | 3–4 hrs |
| 4.4 | **ML Coding Questions** | Implement k-NN, logistic regression, K-means from scratch | ⭐⭐⭐⭐ | 8–10 hrs |
| 4.5 | **Mock Interviews** | Pair practice, timed system design, behavioral STAR stories | ⭐⭐⭐⭐⭐ | 6–8 hrs |
| 4.6 | **Resume & GitHub Polish** | 1-page resume, pinned repos, project READMEs | ⭐⭐⭐⭐ | 4–5 hrs |

### Phase 4 Deliverable

> **[Project 4: End-to-End Deployed Model](projects/04-end-to-end-deployed-model/)**
> 
> Train a model, wrap in FastAPI, containerize with Docker, CI/CD via GitHub Actions.
> 
> **Why this matters:** This is the project that makes you stand out. Most candidates can't deploy.

### After Phase 4, You Can:

- [ ] Build and run a Docker container for an ML API
- [ ] Implement logistic regression from scratch in NumPy
- [ ] Clearly articulate your project decisions in a mock interview
- [ ] Present a resume with quantified project impact
- [ ] Confidently discuss ML tradeoffs: latency vs throughput, precision vs recall

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

1. **Fork this repository**
2. Check off the boxes above as you complete each topic
3. Push your projects to separate GitHub repos
4. Link your projects in your resume
5. Use [`WEEKLY_PLAN.md`](WEEKLY_PLAN.md) for day-by-day structure

---

## Interview-Ready Meaning

Interviewers don't test how many videos you watched. They test whether you can:

1. **Explain** — Can you explain a concept without referring to notes?
2. **Build** — Can you implement an algorithm from scratch?
3. **Reason** — Can you discuss tradeoffs and make engineering decisions?
4. **Deploy** — Can you take a model to production?

This roadmap prepares you for all four.
