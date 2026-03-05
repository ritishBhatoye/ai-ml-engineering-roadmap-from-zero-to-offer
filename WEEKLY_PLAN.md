# 24-Week Study Plan — From Zero to Interview-Ready

> **Time commitment:** 10–15 hours per week (realistic for a student with coursework)
> **Format:** Each week has reading, coding, checkpoint, and deliverable
> **Adjust as needed:** If faster, compress to 12 weeks. If slower, extend to 30 weeks max.

---

## Weekly Time Budget

```
Weekdays (Mon–Fri):  1.5–2 hrs/day  = 7.5–10 hrs
Saturday:            2–3 hrs       = 2–3  hrs
Sunday:              1–2 hrs       = 1–2  hrs
                                    ─────────
Total per week:                      10–15 hrs
```

---

## Phase 1: Foundations (Weeks 1–6)

### Week 1 — Linear Algebra & Python Setup

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`01-mathematics/linear-algebra.md`](01-mathematics/linear-algebra.md) + 3Blue1Brown "Essence of Linear Algebra" (Episodes 1–6) | 3 |
| 💻 Code | Implement matrix multiplication, dot product, transpose from scratch (pure Python). Then re-implement with NumPy and compare | 4 |
| 🛠️ Deliverable | Notebook: `linear_algebra_from_scratch.ipynb` | — |
| ✅ Checkpoint | Can you compute PCA eigenvalues manually? | — |

### Week 2 — Probability & Statistics

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`01-mathematics/probability.md`](01-mathematics/probability.md) + [`01-mathematics/statistics.md`](01-mathematics/statistics.md) | 3 |
| 💻 Code | Simulate coin flips (law of large numbers), compute Bayesian posterior, plot Gaussian/Binomial distributions | 5 |
| 🛠️ Deliverable | Notebook: `probability_simulations.ipynb` | — |
| ✅ Checkpoint | Solve: "A disease affects 1 in 1000. Test is 99% accurate. You test positive. What's P(disease)?" | — |

### Week 3 — Calculus + Gradient Descent

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`01-mathematics/calculus.md`](01-mathematics/calculus.md) + 3Blue1Brown "Essence of Calculus" (Episodes 1–4) | 2 |
| 💻 Code | Implement gradient descent for quadratic. Visualize convergence. Implement for linear regression | 5 |
| 🛠️ Deliverable | Notebook: `gradient_descent_visualized.ipynb` | — |
| ✅ Checkpoint | Can you explain chain rule in backpropagation? | — |

### Week 4 — NumPy, Pandas & Data Manipulation

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`02-python-for-ml/numpy-pandas.md`](02-python-for-ml/numpy-pandas.md) | 2 |
| 💻 Code | Download Titanic dataset. Clean: missing values, encode categoricals, create features, summary stats | 6 |
| 🛠️ Deliverable | Script: `data_cleaning_pipeline.py` + cleaned CSV | — |
| ✅ Checkpoint | Can you use groupby, merge, and pivot_table? | — |

### Week 5 — Visualization & EDA

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`02-python-for-ml/matplotlib-seaborn.md`](02-python-for-ml/matplotlib-seaborn.md) | 2 |
| 💻 Code | Build complete EDA: distributions, correlations, outliers, pair plots. Use Week 4 dataset | 5 |
| 🛠️ Deliverable | **🎯 PROJECT 1: Exploratory Data Analysis** — Push as standalone repo with polished README | — |
| ✅ Checkpoint | Can you create a correlation heatmap and explain insights? | — |

### Week 6 — Supervised Learning: Regression & Classification

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`03-ml-fundamentals/supervised-learning.md`](03-ml-fundamentals/supervised-learning.md) + [`03-ml-fundamentals/evaluation-metrics.md`](03-ml-fundamentals/evaluation-metrics.md) | 3 |
| 💻 Code | Train linear regression, logistic regression, k-NN on Titanic. Compare: accuracy, precision, recall, F1, AUC | 6 |
| 🛠️ Deliverable | Notebook: `supervised_models_comparison.ipynb` with metrics summary table | — |
| ✅ Checkpoint | Can you explain when to use F1 vs AUC? | — |

---

## Phase 2: Core ML Engineering (Weeks 7–14)

### Week 7 — Bias-Variance & Regularization

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`03-ml-fundamentals/bias-variance-tradeoff.md`](03-ml-fundamentals/bias-variance-tradeoff.md) + [`03-ml-fundamentals/regularization.md`](03-ml-fundamentals/regularization.md) | 3 |
| 💻 Code | Polynomial regression degree 1, 5, 15 — plot underfit/overfit. Add Ridge/Lasso, plot coefficient paths | 5 |
| 🛠️ Deliverable | Notebook: `bias_variance_curves.ipynb` with annotated plots | — |
| ✅ Checkpoint | Can you draw the bias-variance tradeoff curve? | — |

### Week 8 — Feature Engineering

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`03-ml-fundamentals/feature-engineering.md`](03-ml-fundamentals/feature-engineering.md) | 2 |
| 💻 Code | Take Ames Housing. Implement: one-hot, target encoding, binning, log transforms, interactions. Build sklearn ColumnTransformer | 6 |
| 🛠️ Deliverable | Module: `feature_pipeline.py` — reusable feature engineering | — |
| ✅ Checkpoint | Can you explain difference between one-hot and target encoding? | — |

### Week 9 — Decision Trees & Ensembles

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`03-ml-fundamentals/supervised-learning.md`](03-ml-fundamentals/supervised-learning.md) — ensemble section | 2 |
| 💻 Code | Train Decision Tree, Random Forest, XGBoost. Tune with GridSearchCV. Compare performance | 6 |
| 🛠️ Deliverable | Notebook: `ensemble_model_shootout.ipynb` | — |
| ✅ Checkpoint | Can you explain difference between bagging and boosting? | — |

### Week 10 — Unsupervised Learning

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`03-ml-fundamentals/unsupervised-learning.md`](03-ml-fundamentals/unsupervised-learning.md) | 2 |
| 💻 Code | Implement K-means from scratch. Apply PCA. Cluster Iris, visualize with t-SNE | 5 |
| 🛠️ Deliverable | Notebook: `clustering_and_pca.ipynb` | — |
| ✅ Checkpoint | Can you explain how to choose number of clusters in K-means? | — |

### Week 11 — SQL for ML

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`05-sql-for-ml/sql-essentials.md`](05-sql-for-ml/sql-essentials.md) | 2 |
| 💻 Code | 20 LeetCode/HackerRank SQL problems. Focus: JOINs, GROUP BY, window functions (ROW_NUMBER, LAG, LEAD), CTEs. Build feature table | 6 |
| 🛠️ Deliverable | File: `sql_practice.sql` — 20 annotated solutions | — |
| ✅ Checkpoint | Can you write a query using window function for ranking? | — |

### Week 12 — Clean ML Code & Pipeline

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`02-python-for-ml/clean-ml-code.md`](02-python-for-ml/clean-ml-code.md) | 2 |
| 💻 Code | Refactor Week 9 notebook: `src/`, `config.yaml`, `train.py`, `evaluate.py`, `requirements.txt` | 5 |
| 🛠️ Deliverable | **🎯 PROJECT 2: Supervised ML Pipeline** — Push as standalone repo | — |
| ✅ Checkpoint | Can you run training from command line with config? | — |

### Week 13 — Cross-Validation & Hyperparameter Tuning

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | Revisit bias-variance + sklearn docs on `cross_val_score`, `RandomizedSearchCV` | 2 |
| 💻 Code | Implement nested cross-validation on Project 2. Compare tuned vs untuned. Analyze overfitting via learning curves | 5 |
| 🛠️ Deliverable | Report: `hyperparameter_tuning_report.md` with learning curves | — |
| ✅ Checkpoint | Can you explain why we use stratified k-fold? | — |

### Week 14 — Review & Consolidation

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | Re-read weak topics from Phase 1–2 | 3 |
| 💻 Code | 10 ML coding questions from [`06-ml-coding/coding-questions.md`](06-ml-coding/coding-questions.md) | 5 |
| 🛠️ Deliverable | File: `ml_coding_solutions.py` | — |
| ✅ Checkpoint | Can you implement k-NN from scratch in 15 minutes? | — |

---

## Phase 3: Deep Learning + System Design (Weeks 15–20)

### Week 15 — Neural Network Basics

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`04-deep-learning/neural-network-basics.md`](04-deep-learning/neural-network-basics.md) | 3 |
| 💻 Code | Build 2-layer NN from scratch in NumPy for binary classification. Re-implement in PyTorch. Compare | 6 |
| 🛠️ Deliverable | Notebook: `nn_from_scratch_vs_pytorch.ipynb` | — |
| ✅ Checkpoint | Can you derive backpropagation for a simple network? | — |

### Week 16 — Convolutional Neural Networks

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`04-deep-learning/cnn.md`](04-deep-learning/cnn.md) | 3 |
| 💻 Code | Build CNN for CIFAR-10 in PyTorch. Experiment: layers, kernels, dropout, batch norm. Plot training curves | 6 |
| 🛠️ Deliverable | **🎯 PROJECT 3: Deep Learning Classifier** — Push as standalone repo | — |
| ✅ Checkpoint | Can you explain what convolutions learn? | — |

### Week 17 — RNNs & LSTMs

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`04-deep-learning/rnn-lstm.md`](04-deep-learning/rnn-lstm.md) | 3 |
| 💻 Code | Build LSTM for IMDB sentiment analysis. Compare with simple RNN. Visualize vanishing gradients | 5 |
| 🛠️ Deliverable | Notebook: `rnn_vs_lstm_sentiment.ipynb` | — |
| ✅ Checkpoint | Can you explain LSTM gates and why they help? | — |

### Week 18 — Transformers

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`04-deep-learning/transformers.md`](04-deep-learning/transformers.md) + "The Illustrated Transformer" | 3 |
| 💻 Code | Fine-tune DistilBERT on text classification using HuggingFace Transformers | 5 |
| 🛠️ Deliverable | Notebook: `transformer_finetuning.ipynb` | — |
| ✅ Checkpoint | Can you explain self-attention mechanism? | — |

### Week 19 — ML System Design & Data Leakage

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`08-system-design/ml-pipeline-design.md`](08-system-design/ml-pipeline-design.md) + [`08-system-design/data-leakage.md`](08-system-design/data-leakage.md) | 3 |
| 💻 Code | Draw full ML pipeline for recommendation system. Identify 3 leakage scenarios in example datasets | 4 |
| 🛠️ Deliverable | Document: `system_design_exercise.md` with pipeline diagram | — |
| ✅ Checkpoint | Can you identify 3 types of data leakage? | — |

### Week 20 — Case Studies

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | All files in [`07-case-studies/`](07-case-studies/) | 4 |
| 💻 Code | Implement spam classifier end-to-end: data → preprocessing → model → evaluation → simple API | 6 |
| 🛠️ Deliverable | Notebook: `spam_classifier_case_study.ipynb` | — |
| ✅ Checkpoint | Can you design an ML system end-to-end? | — |

---

## Phase 4: Deployment + Interview Sprint (Weeks 21–24)

### Week 21 — Flask/FastAPI for ML

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`09-deployment/flask-fastapi.md`](09-deployment/flask-fastapi.md) | 2 |
| 💻 Code | Wrap spam classifier in FastAPI. Add `/predict` endpoint, Pydantic validation, `/health` check | 5 |
| 🛠️ Deliverable | Files: `app.py`, `model.py`, `requirements.txt`, `tests/` | — |
| ✅ Checkpoint | Can you call your API with curl? | — |

### Week 22 — Docker & Cloud Basics

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`09-deployment/docker-basics.md`](09-deployment/docker-basics.md) + [`09-deployment/cloud-overview.md`](09-deployment/cloud-overview.md) | 3 |
| 💻 Code | Write Dockerfile and docker-compose for FastAPI app. Build, run, test locally. Optional: deploy to AWS EC2 | 5 |
| 🛠️ Deliverable | **🎯 PROJECT 4: End-to-End Deployed Model** — Push as standalone repo with Docker | — |
| ✅ Checkpoint | Can you run your API in a Docker container? | — |

### Week 23 — Interview Question Sprint

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`INTERVIEW_PREP.md`](INTERVIEW_PREP.md) + [`10-interview-strategy/interview-questions.md`](10-interview-strategy/interview-questions.md) — all categories | 3 |
| 💻 Code | 15 more ML coding questions. Practice explaining out loud (record yourself) | 6 |
| 🛠️ Deliverable | File: `coding_sprint_solutions.py` | — |
| ✅ Checkpoint | Can you answer 20 theory questions in 2 minutes each? | — |

### Week 24 — Resume, GitHub & Mock Interviews

| Block | Activity | Hours |
|-------|----------|:-----:|
| 📖 Read | [`10-interview-strategy/resume-strategy.md`](10-interview-strategy/resume-strategy.md) + [`10-interview-strategy/github-profile.md`](10-interview-strategy/github-profile.md) | 2 |
| 💻 Code | Polish all 4 project repos: add badges, clean READMEs, requirements.txt, screenshots | 3 |
| 🎤 Practice | 2 mock interviews (friend, peer, or Pramp). One ML theory + one coding | 4 |
| 🛠️ Deliverable | Finalized 1-page resume (PDF) + polished GitHub profile | — |
| ✅ Checkpoint | Have you completed 4+ mock interviews? | — |

---

## Compressed 12-Week Plan (3 Months)

If you only have 3 months, compress as follows:

| Week | Original Weeks | Focus | Checkpoint |
|:----:|:--------------:|-------|------------|
| 1–2 | 1–4 | Math + Python (skim, focus on gaps) | Can you clean data in pandas? |
| 3–4 | 5–6 | EDA project + supervised learning | Project 1 complete |
| 5–6 | 7–9 | Feature engineering + ensembles | Can you tune XGBoost? |
| 7–8 | 10–11 | Unsupervised + SQL | Can you write window functions? |
| 9 | 15–16 | Neural networks + CNN project | Project 3 complete |
| 10 | 17–18 | RNN + Transformers | Can you fine-tune BERT? |
| 11 | 19–22 | System design + deployment | Project 4 complete |
| 12 | 23–24 | Interview sprint + mock interviews | Resume ready |

---

## Key Principles

1. **Consistency beats intensity** — 10 hrs/week for 6 months > 40 hrs/week for 1 month
2. **Build every project** — Code is your proof
3. **Explain out loud** — Record yourself answering questions
4. **Start interviewing early** — Don't wait until "you're ready"
5. **Review weekly** — Sundays: 1 hour review of week's work

---

## Evaluation Checkpoints Summary

| Phase | Checkpoint | How to Verify |
|-------|------------|---------------|
| 1 | Math fundamentals | Solve 5 probability problems |
| 1 | Data manipulation | Clean Titanic from scratch |
| 1 | Model training | Train 3 models on Titanic |
| 2 | Feature engineering | Build ColumnTransformer pipeline |
| 2 | Ensemble methods | Tune XGBoost with CV |
| 2 | SQL queries | Solve 20 SQL problems |
| 3 | Deep learning | Train CNN from scratch |
| 3 | System design | Draw pipeline on whiteboard |
| 4 | Deployment | Run API in Docker |
| 4 | Interview ready | Complete 4 mock interviews |

---

> **The plan is useless if you don't follow it. The follow-through is everything.**
