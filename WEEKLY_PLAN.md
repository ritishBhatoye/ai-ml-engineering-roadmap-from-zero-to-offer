<![CDATA[# 📅 24-Week Study Plan — From Zero to Interview-Ready

> **Time commitment:** 10–15 hours per week.  
> **Format:** Each week has a reading block, a coding block, and a deliverable you can push to GitHub.  
> **Adjust as needed:** If you're faster, compress Phase 1 into 4 weeks. If slower, extend to 30 weeks max.

---

## Phase 1: Foundations (Weeks 1–6)

### Week 1 — Linear Algebra & Python Setup

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`01-mathematics/linear-algebra.md`](01-mathematics/linear-algebra.md) + 3Blue1Brown "Essence of Linear Algebra" (Episodes 1–6) | 3 |
| 💻 Code | Implement matrix multiplication, dot product, and transpose from scratch (no NumPy). Then re-implement with NumPy and compare | 4 |
| 🛠️ Deliverable | Notebook: `linear_algebra_from_scratch.ipynb` | — |

### Week 2 — Probability & Statistics

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`01-mathematics/probability.md`](01-mathematics/probability.md) + [`01-mathematics/statistics.md`](01-mathematics/statistics.md) | 3 |
| 💻 Code | Simulate coin flips (law of large numbers), compute Bayesian posterior for a simple example, plot distributions (Gaussian, Binomial) | 5 |
| 🛠️ Deliverable | Notebook: `probability_simulations.ipynb` | — |

### Week 3 — Calculus + Gradient Descent

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`01-mathematics/calculus.md`](01-mathematics/calculus.md) + 3Blue1Brown "Essence of Calculus" (Episodes 1–4) | 2 |
| 💻 Code | Implement gradient descent for a simple quadratic function. Visualize the convergence path. Then implement it for linear regression | 5 |
| 🛠️ Deliverable | Notebook: `gradient_descent_visualized.ipynb` | — |

### Week 4 — NumPy, Pandas & Data Manipulation

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`02-python-for-ml/numpy-pandas.md`](02-python-for-ml/numpy-pandas.md) | 2 |
| 💻 Code | Download a messy Kaggle dataset (e.g., Titanic). Clean it: handle missing values, encode categoricals, create new features, produce summary stats | 6 |
| 🛠️ Deliverable | Script: `data_cleaning_pipeline.py` + cleaned CSV output | — |

### Week 5 — Visualization & EDA

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`02-python-for-ml/matplotlib-seaborn.md`](02-python-for-ml/matplotlib-seaborn.md) | 2 |
| 💻 Code | Build a complete EDA report: distributions, correlations, outlier detection, pair plots. Use the dataset from Week 4 | 5 |
| 🛠️ Deliverable | **🎯 PROJECT 1: Exploratory Data Analysis** — Push as a standalone repo with a polished README | — |

### Week 6 — Supervised Learning: Regression & Classification

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`03-ml-fundamentals/supervised-learning.md`](03-ml-fundamentals/supervised-learning.md) + [`03-ml-fundamentals/evaluation-metrics.md`](03-ml-fundamentals/evaluation-metrics.md) | 3 |
| 💻 Code | Train linear regression (from scratch + sklearn), logistic regression, and k-NN on the Titanic dataset. Compare metrics: accuracy, precision, recall, F1, AUC | 6 |
| 🛠️ Deliverable | Notebook: `supervised_models_comparison.ipynb` with a metrics summary table | — |

---

## Phase 2: Core ML Engineering (Weeks 7–14)

### Week 7 — Bias-Variance & Regularization

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`03-ml-fundamentals/bias-variance-tradeoff.md`](03-ml-fundamentals/bias-variance-tradeoff.md) + [`03-ml-fundamentals/regularization.md`](03-ml-fundamentals/regularization.md) | 3 |
| 💻 Code | Polynomial regression with degree 1, 5, 15 — plot underfitting, good fit, overfitting. Add Ridge/Lasso and plot coefficient paths | 5 |
| 🛠️ Deliverable | Notebook: `bias_variance_curves.ipynb` with annotated plots | — |

### Week 8 — Feature Engineering

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`03-ml-fundamentals/feature-engineering.md`](03-ml-fundamentals/feature-engineering.md) | 2 |
| 💻 Code | Take a raw dataset (e.g., Ames Housing). Implement: one-hot encoding, target encoding, binning, log transforms, interaction features, feature selection (mutual information). Build sklearn `ColumnTransformer` | 6 |
| 🛠️ Deliverable | Module: `feature_pipeline.py` — reusable feature engineering pipeline | — |

### Week 9 — Decision Trees & Ensembles

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`03-ml-fundamentals/supervised-learning.md`](03-ml-fundamentals/supervised-learning.md) — ensemble section | 2 |
| 💻 Code | Train Decision Tree, Random Forest, and XGBoost. Tune hyperparameters with GridSearchCV. Compare performance | 6 |
| 🛠️ Deliverable | Notebook: `ensemble_model_shootout.ipynb` | — |

### Week 10 — Unsupervised Learning

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`03-ml-fundamentals/unsupervised-learning.md`](03-ml-fundamentals/unsupervised-learning.md) | 2 |
| 💻 Code | Implement K-means from scratch. Apply PCA for dimensionality reduction. Cluster the Iris dataset and visualize with t-SNE | 5 |
| 🛠️ Deliverable | Notebook: `clustering_and_pca.ipynb` | — |

### Week 11 — SQL for ML

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`05-sql-for-ml/sql-essentials.md`](05-sql-for-ml/sql-essentials.md) | 2 |
| 💻 Code | Practice 20 SQL problems on LeetCode/HackerRank. Focus on: JOINs, GROUP BY, window functions (ROW_NUMBER, LAG, LEAD), CTEs. Create a feature table from a transactional database | 6 |
| 🛠️ Deliverable | File: `sql_practice.sql` — 20 annotated solutions | — |

### Week 12 — Clean ML Code

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`02-python-for-ml/clean-ml-code.md`](02-python-for-ml/clean-ml-code.md) | 2 |
| 💻 Code | Refactor your Week 9 notebook into a modular project: `src/`, `config.yaml`, `train.py`, `evaluate.py`, `requirements.txt` | 5 |
| 🛠️ Deliverable | **🎯 PROJECT 2: Supervised ML Pipeline** — Push as a standalone repo | — |

### Week 13 — Cross-Validation & Hyperparameter Tuning

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | Revisit bias-variance + sklearn docs on `cross_val_score`, `RandomizedSearchCV` | 2 |
| 💻 Code | Implement nested cross-validation on your project. Compare results with/without hyperparameter tuning. Analyse overfitting via learning curves | 5 |
| 🛠️ Deliverable | Report: `hyperparameter_tuning_report.md` — including learning curves | — |

### Week 14 — Review & Consolidation

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | Re-read any weak topics from Phase 1–2 | 3 |
| 💻 Code | Complete 10 ML coding questions from [`06-ml-coding/coding-questions.md`](06-ml-coding/coding-questions.md) | 5 |
| 🛠️ Deliverable | File: `ml_coding_solutions.py` | — |

---

## Phase 3: Deep Learning + System Design (Weeks 15–20)

### Week 15 — Neural Network Basics

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`04-deep-learning/neural-network-basics.md`](04-deep-learning/neural-network-basics.md) | 3 |
| 💻 Code | Build a 2-layer neural network from scratch in NumPy for binary classification. Then re-implement in PyTorch. Compare results | 6 |
| 🛠️ Deliverable | Notebook: `nn_from_scratch_vs_pytorch.ipynb` | — |

### Week 16 — Convolutional Neural Networks

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`04-deep-learning/cnn.md`](04-deep-learning/cnn.md) | 3 |
| 💻 Code | Build a CNN in PyTorch for CIFAR-10. Experiment with: number of layers, kernel sizes, dropout, batch normalization. Plot training curves | 6 |
| 🛠️ Deliverable | **🎯 PROJECT 3: Deep Learning Classifier** — Push as standalone repo | — |

### Week 17 — RNNs & LSTMs

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`04-deep-learning/rnn-lstm.md`](04-deep-learning/rnn-lstm.md) | 3 |
| 💻 Code | Build an LSTM for text classification (e.g., sentiment analysis on IMDB). Compare with a simple RNN. Visualize vanishing gradient problem | 5 |
| 🛠️ Deliverable | Notebook: `rnn_vs_lstm_sentiment.ipynb` | — |

### Week 18 — Transformers

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`04-deep-learning/transformers.md`](04-deep-learning/transformers.md) + "The Illustrated Transformer" blog | 3 |
| 💻 Code | Fine-tune a pretrained DistilBERT on a text classification task using HuggingFace Transformers library | 5 |
| 🛠️ Deliverable | Notebook: `transformer_finetuning.ipynb` | — |

### Week 19 — ML System Design & Data Leakage

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`08-system-design/ml-pipeline-design.md`](08-system-design/ml-pipeline-design.md) + [`08-system-design/data-leakage.md`](08-system-design/data-leakage.md) | 3 |
| 💻 Code | Draw a full ML pipeline diagram for a recommendation system. Identify potential leakage points in 3 example datasets | 4 |
| 🛠️ Deliverable | Document: `system_design_exercise.md` with pipeline diagram (draw.io or Excalidraw) | — |

### Week 20 — Case Studies

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | All files in [`07-case-studies/`](07-case-studies/) | 4 |
| 💻 Code | Implement the spam classifier case study end-to-end: data → preprocessing → model → evaluation → simple API | 6 |
| 🛠️ Deliverable | Notebook: `spam_classifier_case_study.ipynb` | — |

---

## Phase 4: Deployment + Interview Sprint (Weeks 21–24)

### Week 21 — Flask/FastAPI for ML

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`09-deployment/flask-fastapi.md`](09-deployment/flask-fastapi.md) | 2 |
| 💻 Code | Wrap your spam classifier in a FastAPI app. Add `/predict` endpoint, input validation with Pydantic, and `/health` endpoint | 5 |
| 🛠️ Deliverable | Files: `app.py`, `model.py`, `requirements.txt` | — |

### Week 22 — Docker & Cloud Basics

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`09-deployment/docker-basics.md`](09-deployment/docker-basics.md) + [`09-deployment/cloud-overview.md`](09-deployment/cloud-overview.md) | 3 |
| 💻 Code | Write a Dockerfile and docker-compose for your FastAPI app. Build, run, and test locally. (Optional: deploy to an AWS EC2 free tier instance) | 5 |
| 🛠️ Deliverable | **🎯 PROJECT 4: End-to-End Deployed Model** — Push as standalone repo with Docker support | — |

### Week 23 — Interview Question Sprint

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`10-interview-strategy/interview-questions.md`](10-interview-strategy/interview-questions.md) — attempt all categories | 3 |
| 💻 Code | Complete 15 more ML coding questions. Practice explaining solutions out loud (record yourself) | 6 |
| 🛠️ Deliverable | File: `coding_sprint_solutions.py` | — |

### Week 24 — Resume, GitHub & Mock Interviews

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`10-interview-strategy/resume-strategy.md`](10-interview-strategy/resume-strategy.md) + [`10-interview-strategy/github-profile.md`](10-interview-strategy/github-profile.md) | 2 |
| 💻 Code | Polish all 4 project repos: add badges, clean READMEs, add `requirements.txt`, add screenshots/results | 3 |
| 🎤 Practice | Do 2 mock interviews (with a friend, peer, or on Pramp). One ML theory + one coding | 4 |
| 🛠️ Deliverable | Finalized 1-page resume (PDF) + polished GitHub profile | — |

---

## Quick Reference: Weekly Time Budget

```
Mon–Fri (weekdays):  1.5–2 hrs/day = 7.5–10 hrs
Saturday:            2–3 hrs       = 2–3  hrs
Sunday:              1–2 hrs       = 1–2  hrs
                                   ─────────
Total:                              10–15 hrs/week
```

---

## If You Only Have 3 Months (12 Weeks)

Compress the plan:

| Compressed Week | Original Weeks | Focus |
|:---:|:---:|---|
| 1–2 | 1–4 | Math + Python (skim, focus on gaps) |
| 3–4 | 5–6 | EDA project + supervised learning |
| 5–6 | 7–9 | Feature engineering + ensembles |
| 7–8 | 10–11 | Unsupervised + SQL |
| 9 | 15–16 | Neural networks + CNN project |
| 10 | 17–18 | RNN + Transformers |
| 11 | 19–22 | System design + deployment |
| 12 | 23–24 | Interview sprint + mock interviews |

---

> **The plan is useless if you don't follow it. The follow-through is everything.**
]]>
