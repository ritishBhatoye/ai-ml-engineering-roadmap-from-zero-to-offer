# Project 1: Exploratory Data Analysis & Visualization

## Objective

Perform a comprehensive EDA on a real-world dataset. Demonstrate that you can clean, explore, and extract insights from messy data.

**Why this matters:** Data cleaning and EDA are 80% of real ML work. Interviewers want to see you can work with messy data.

---

## Suggested Datasets

| Dataset | Use Case | Source |
|---------|----------|--------|
| Titanic Survival | Binary classification, beginner-friendly | [Kaggle](https://www.kaggle.com/c/titanic) |
| House Prices | Regression, feature engineering | [Kaggle](https://www.kaggle.com/c/house-prices-advanced-regression-techniques) |
| COVID-19 Open Data | Time series, large-scale | [Google Cloud](https://github.com/GoogleCloudPlatform/covid-19-open-data) |
| Retail Sales | Time series, business insights | [Kaggle](https://www.kaggle.com/competitions/retail-sales-forecasting) |

---

## Deliverables Checklist

### Data Processing
- [ ] Data loading and inspection — shape, dtypes, nulls, summary stats
- [ ] Missing value analysis — visualize missing patterns, implement imputation strategy
- [ ] Data type conversions — handle strings, dates, categoricals

### Analysis
- [ ] Univariate analysis — distributions of each feature (histograms, box plots)
- [ ] Bivariate analysis — correlations, scatter plots, grouped comparisons
- [ ] Outlier detection — identify and handle outliers with justification

### Feature Engineering
- [ ] Create 3+ new features with domain reasoning
- [ ] Document feature engineering rationale

### Communication
- [ ] Key insights — 5+ findings with supporting visualizations
- [ ] Clean README — problem description, approach, key findings, how to run

---

## Assessment Criteria

| Criterion | Weight | What Interviewers Look For |
|-----------|--------|---------------------------|
| Data Cleaning | 25% | Handles missing values, outliers, wrong data types appropriately |
| Visualizations | 25% | Clear, informative plots that tell a story |
| Insights | 25% | Actionable findings that could inform business decisions |
| Code Quality | 15% | Clean, documented, reproducible code |
| Communication | 10% | Clear README, well-organized repo |

---

## Suggested Structure

```
01-eda-project/
├── data/
│   ├── raw/                    # Original data (or download script)
│   └── processed/              # Cleaned data
├── notebooks/
│   └── eda.ipynb               # Main analysis
├── src/
│   └── utils.py               # Helper functions
├── images/                    # Saved plots for README
├── requirements.txt
└── README.md
```

---

## Starter Code

```python
# src/utils.py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

def load_data(path: str) -> pd.DataFrame:
    """Load CSV and show basic info."""
    df = pd.read_csv(path)
    print(f"Shape: {df.shape}")
    print(f"\nData types:\n{df.dtypes}")
    print(f"\nMissing values:\n{df.isnull().sum()}")
    return df

def summarize_numeric(df: pd.DataFrame) -> pd.DataFrame:
    """Summary statistics for numeric columns."""
    return df.describe()

def plot_correlation_matrix(df: pd.DataFrame, save_path: str = None):
    """Plot heatmap of correlations."""
    numeric_df = df.select_dtypes(include=[np.number])
    plt.figure(figsize=(10, 8))
    sns.heatmap(numeric_df.corr(), annot=True, cmap='coolwarm', fmt='.2f')
    plt.title('Correlation Matrix')
    if save_path:
        plt.savefig(save_path)
    plt.show()
```

---

## Estimated Time: 8–12 hours
