# Learning Roadmap — Beginner to Interview-Ready

> This roadmap is designed for a student with 3–6 months of dedicated preparation.
> Every topic maps directly to what interviewers test in ML internships and entry-level roles.

---

## How to Read This Roadmap

- **Each phase** builds on the previous — don't skip ahead
- **Checkboxes** are for your own tracking — fork this repo and check them off
- **"Interview Signal"** tells you how heavily this topic is tested (1-5 stars)
- **"Practical Exercise"** gives you hands-on practice for each topic
- **"Time Investment"** is a realistic estimate including practice

---

## Phase 1: Foundations (Weeks 1–6)

**Goal:** Master the math behind ML, write production-quality Python data code, and train your first models with proper evaluation.

### Topics

| # | Topic | Key Concepts | Interview Signal | Practical Exercise | Time |
|---|-------|-------------|:---:|---|:---:|
| 1.1 | **Linear Algebra** | Vectors, matrices, eigenvalues, SVD | ⭐⭐⭐ | Implement PCA from scratch using numpy | 4–5 hrs |
| 1.2 | **Probability** | Bayes' theorem, distributions, expectation | ⭐⭐⭐⭐ | Build a Bayesian spam classifier | 5–6 hrs |
| 1.3 | **Statistics** | Hypothesis testing, p-values, confidence intervals | ⭐⭐⭐ | A/B test analysis on conversion data | 4–5 hrs |
| 1.4 | **Calculus** | Derivatives, chain rule, gradient descent | ⭐⭐ | Implement gradient descent for linear regression | 3–4 hrs |
| 1.5 | **NumPy & Pandas** | Array operations, DataFrames, merge | ⭐⭐⭐⭐ | Clean and transform Titanic dataset | 6–8 hrs |
| 1.6 | **Matplotlib & Seaborn** | Histograms, scatter plots, heatmaps | ⭐⭐ | Create complete EDA visualization report | 3–4 hrs |
| 1.7 | **Supervised Learning** | Linear regression, logistic regression, k-NN | ⭐⭐⭐⭐⭐ | Train and compare 3 models on Titanic | 8–10 hrs |
| 1.8 | **Evaluation Metrics** | Accuracy, precision, recall, F1, AUC | ⭐⭐⭐⭐⭐ | Build a metrics dashboard for model comparison | 4–5 hrs |

### Learning Outcomes

After Phase 1, you can:
- [ ] Explain gradient descent to a non-technical person
- [ ] Write a pandas pipeline to clean and transform raw CSV data
- [ ] Train a logistic regression classifier and evaluate it properly
- [ ] Explain precision vs recall tradeoff with a real example (fraud detection)
- [ ] Solve basic probability interview questions (Bayes, conditional probability)

### Phase 1 Deliverable

> **[Project 1: Exploratory Data Analysis](projects/01-eda-and-visualization/)**
> 
> - Clean a messy dataset (Titanic, House Prices, or your choice)
> - Generate 5+ key insights with visualizations
> - Push to GitHub with polished README

---

## Phase 2: Core ML Engineering (Weeks 7–14)

**Goal:** Master the full classical ML toolkit, understand feature engineering deeply, and write SQL for data extraction.

### Topics

| # | Topic | Key Concepts | Interview Signal | Practical Exercise | Time |
|---|-------|-------------|:---:|---|:---:|
| 2.1 | **Bias-Variance** | Underfitting vs overfitting, generalization | ⭐⭐⭐⭐⭐ | Plot learning curves for polynomial regression | 3–4 hrs |
| 2.2 | **Regularization** | L1 (Lasso), L2 (Ridge), elastic net | ⭐⭐⭐⭐ | Compare Ridge vs Lasso on high-dimensional data | 4–5 hrs |
| 2.3 | **Feature Engineering** | Encoding, scaling, binning, selection | ⭐⭐⭐⭐⭐ | Build sklearn ColumnTransformer pipeline | 6–8 hrs |
| 2.4 | **Unsupervised Learning** | K-means, hierarchical, PCA, DBSCAN | ⭐⭐⭐ | Customer segmentation on retail data | 5–6 hrs |
| 2.5 | **Ensemble Methods** | Random Forest, XGBoost, LightGBM, stacking | ⭐⭐⭐⭐⭐ | Build XGBoost model with hyperparameter tuning | 6–8 hrs |
| 2.6 | **Cross-Validation** | K-fold, stratified, time-series split | ⭐⭐⭐⭐ | Implement nested cross-validation | 3–4 hrs |
| 2.7 | **SQL for ML** | Joins, window functions, CTEs, aggregations | ⭐⭐⭐⭐ | Write queries to build feature tables | 6–8 hrs |
| 2.8 | **Clean ML Code** | Modular scripts, type hints, config, reproducibility | ⭐⭐⭐ | Refactor notebook into production-style project | 4–5 hrs |

### Learning Outcomes

After Phase 2, you can:
- [ ] Explain why XGBoost typically outperforms vanilla decision trees
- [ ] Write a sklearn pipeline with preprocessing and model training
- [ ] Discuss feature engineering strategies for categorical vs numerical features
- [ ] Write SQL queries with window functions to build feature tables
- [ ] Explain L1 vs L2 regularization and when to use each

### Phase 2 Deliverable

> **[Project 2: Supervised ML Pipeline](projects/02-supervised-ml-pipeline/)**
> 
> - Build complete ML pipeline: preprocessing → features → model → tuning
> - Compare 3+ models with proper evaluation
> - Push to GitHub with modular code structure

---

## Phase 3: Deep Learning + System Design (Weeks 15–20)

**Goal:** Understand modern deep learning architectures and how ML systems work in production.

### Topics

| # | Topic | Key Concepts | Interview Signal | Practical Exercise | Time |
|---|-------|-------------|:---:|---|:---:|
| 3.1 | **Neural Network Basics** | Perceptrons, backprop, activations | ⭐⭐⭐⭐ | Build 2-layer NN from scratch in NumPy | 5–6 hrs |
| 3.2 | **CNNs** | Convolution, pooling, ResNet, transfer learning | ⭐⭐⭐⭐ | Train CNN on CIFAR-10, compare with pretrained | 6–8 hrs |
| 3.3 | **RNNs & LSTMs** | Sequence modeling, vanishing gradients | ⭐⭐⭐ | Build LSTM for IMDB sentiment analysis | 5–6 hrs |
| 3.4 | **Transformers** | Self-attention, BERT, GPT | ⭐⭐⭐⭐ | Fine-tune DistilBERT for text classification | 5–6 hrs |
| 3.5 | **ML Pipeline Design** | Data → features → training → serving → monitoring | ⭐⭐⭐⭐ | Design pipeline for recommendation system | 5–6 hrs |
| 3.6 | **Data Leakage** | Types, detection, prevention | ⭐⭐⭐⭐⭐ | Identify leakage in 3 real datasets | 3–4 hrs |
| 3.7 | **Monitoring & Drift** | Data drift, concept drift, PSI | ⭐⭐⭐ | Implement drift detection for deployed model | 4–5 hrs |
| 3.8 | **Case Studies** | Recommendation, spam, credit risk | ⭐⭐⭐⭐ | Implement end-to-end case study | 8–10 hrs |

### Learning Outcomes

After Phase 3, you can:
- [ ] Draw and explain the architecture of a basic CNN
- [ ] Explain why transformers replaced RNNs for most NLP tasks
- [ ] Design an ML pipeline on a whiteboard (data → features → model → serving)
- [ ] Identify 3 types of data leakage in a given dataset
- [ ] Discuss how you would monitor a deployed model for drift

### Phase 3 Deliverable

> **[Project 3: Deep Learning Classifier](projects/03-deep-learning-classifier/)**
> 
> - Train CNN or fine-tune transformer on image/text data
> - Include training curves, confusion matrix, error analysis
> - Push to GitHub with pretrained model comparison

---

## Phase 4: Deployment + Interview Sprint (Weeks 21–24)

**Goal:** Deploy a model, polish your portfolio, and perform at interview level.

### Topics

| # | Topic | Key Concepts | Interview Signal | Practical Exercise | Time |
|---|-------|-------------|:---:|---|:---:|
| 4.1 | **Flask / FastAPI** | REST API, request/response, async | ⭐⭐⭐ | Wrap model in FastAPI with Pydantic validation | 5–6 hrs |
| 4.2 | **Docker** | Dockerfile, multi-stage builds, docker-compose | ⭐⭐⭐ | Containerize FastAPI app | 4–5 hrs |
| 4.3 | **Cloud Basics** | AWS SageMaker, GCP Vertex AI, S3, EC2 | ⭐⭐ | Deploy to cloud (optional) | 3–4 hrs |
| 4.4 | **ML Coding Questions** | Implement k-NN, logistic regression, K-means | ⭐⭐⭐⭐ | Solve 20 LeetCode-style ML problems | 8–10 hrs |
| 4.5 | **Mock Interviews** | Pair practice, timed system design, behavioral | ⭐⭐⭐⭐⭐ | Complete 4+ mock interviews | 6–8 hrs |
| 4.6 | **Resume & GitHub Polish** | 1-page resume, pinned repos, READMEs | ⭐⭐⭐⭐ | Finalize portfolio | 4–5 hrs |

### Learning Outcomes

After Phase 4, you can:
- [ ] Build and run a Docker container for an ML API
- [ ] Implement logistic regression from scratch in NumPy
- [ ] Clearly articulate project decisions in a mock interview
- [ ] Present a resume with quantified project impact
- [ ] Confidently discuss ML tradeoffs: latency vs throughput, precision vs recall

### Phase 4 Deliverable

> **[Project 4: End-to-End Deployed Model](projects/04-end-to-end-deployed-model/)**
> 
> - Train model → FastAPI API → Docker container → CI/CD
> - Deploy to cloud (optional)
> - Complete portfolio with polished README

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

## Interview-Ready Definition

Interviewers don't test how many videos you watched. They test whether you can:

1. **Explain** — Can you explain a concept without referring to notes?
2. **Build** — Can you implement an algorithm from scratch?
3. **Reason** — Can you discuss tradeoffs and make engineering decisions?
4. **Deploy** — Can you take a model to production?

This roadmap prepares you for all four.
