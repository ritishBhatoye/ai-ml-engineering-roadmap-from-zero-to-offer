<![CDATA[# NumPy & Pandas — The ML Engineer's Daily Tools

> **Interview weight:** ⭐⭐⭐⭐ — Tested in live coding rounds and take-home assignments.  
> **Time to study:** 6–8 hours.  
> **Goal:** Manipulate data efficiently without falling into common pitfalls.

---

## NumPy Essentials

### Array Creation & Operations

```python
import numpy as np

# Creation
a = np.array([1, 2, 3])                    # From list
b = np.zeros((3, 4))                        # 3×4 zeros
c = np.ones((2, 3))                         # 2×3 ones
d = np.arange(0, 10, 2)                     # [0, 2, 4, 6, 8]
e = np.linspace(0, 1, 5)                    # 5 evenly spaced: [0, 0.25, 0.5, 0.75, 1]
f = np.random.randn(3, 4)                   # 3×4 from standard normal
g = np.eye(3)                               # 3×3 identity

# Shape manipulation
X = np.random.randn(100, 5)
print(X.shape)           # (100, 5)
X_flat = X.reshape(-1)   # Flatten to 1D: (500,)
X_T = X.T                # Transpose: (5, 100)
```

### Broadcasting – The Most Common Source of Bugs

```python
# Broadcasting lets you do operations on arrays of different shapes
a = np.array([[1], [2], [3]])   # Shape: (3, 1)
b = np.array([10, 20, 30])     # Shape: (3,) → broadcasted to (1, 3)
c = a + b                       # Shape: (3, 3) — OK

# DANGER: Unexpected broadcasting
x = np.array([1, 2, 3])         # Shape: (3,)
y = np.array([1, 2])            # Shape: (2,)
# z = x + y → ERROR! Shapes (3,) and (2,) are incompatible

# Common fix: be explicit about shapes
x = x.reshape(-1, 1)            # (3, 1) — column vector
```

**Interview insight:** When debugging ML code, shape mismatches due to broadcasting are the #1 source of silent bugs. Always print shapes.

### Vectorization — Avoid Loops

```python
# BAD: Python loop
result = []
for i in range(len(X)):
    result.append(np.dot(X[i], w))

# GOOD: Vectorized
result = X @ w   # 100x faster for large arrays
```

### Useful Operations for ML

```python
# Normalize features (zero mean, unit variance)
X_norm = (X - X.mean(axis=0)) / X.std(axis=0)

# Softmax function
def softmax(z):
    exp_z = np.exp(z - np.max(z))  # Subtract max for numerical stability
    return exp_z / exp_z.sum()

# Sigmoid function
def sigmoid(z):
    return 1 / (1 + np.exp(-z))

# One-hot encoding
labels = np.array([0, 2, 1, 0])
one_hot = np.eye(3)[labels]
# [[1,0,0], [0,0,1], [0,1,0], [1,0,0]]
```

---

## Pandas Essentials

### Loading & Inspecting Data

```python
import pandas as pd

df = pd.read_csv("data.csv")

# First things to run on ANY dataset
df.shape                    # (rows, cols)
df.head()                   # First 5 rows
df.info()                   # Column types, non-null counts
df.describe()               # Summary stats for numeric columns
df.isnull().sum()           # Missing values per column
df.dtypes                   # Data types
df.nunique()                # Unique values per column
```

### Data Cleaning Pipeline

```python
# 1. Handle missing values
df["age"].fillna(df["age"].median(), inplace=True)     # Numeric: fill with median
df["city"].fillna("Unknown", inplace=True)             # Categorical: fill with placeholder
df.dropna(subset=["target"], inplace=True)             # Drop rows where target is missing

# 2. Remove duplicates
df.drop_duplicates(inplace=True)

# 3. Fix data types
df["date"] = pd.to_datetime(df["date"])
df["category"] = df["category"].astype("category")

# 4. Handle outliers (IQR method)
Q1 = df["income"].quantile(0.25)
Q3 = df["income"].quantile(0.75)
IQR = Q3 - Q1
df = df[(df["income"] >= Q1 - 1.5 * IQR) & (df["income"] <= Q3 + 1.5 * IQR)]
```

### GroupBy — The Most Powerful Pandas Operation

```python
# Revenue per category
df.groupby("category")["revenue"].agg(["mean", "sum", "count"])

# Multi-level groupby
df.groupby(["year", "category"])["revenue"].mean().unstack()

# Custom aggregation
df.groupby("user_id").agg(
    total_purchases=("amount", "sum"),
    avg_purchase=("amount", "mean"),
    first_purchase=("date", "min"),
    last_purchase=("date", "max"),
    num_transactions=("amount", "count"),
)
```

### Merge & Join

```python
# Inner join (only matching rows)
merged = pd.merge(users, orders, on="user_id", how="inner")

# Left join (keep all users, even without orders)
merged = pd.merge(users, orders, on="user_id", how="left")

# Multiple join keys
merged = pd.merge(df1, df2, on=["user_id", "date"], how="left")
```

### Feature Engineering with Pandas

```python
# Date features
df["day_of_week"] = df["date"].dt.dayofweek
df["month"] = df["date"].dt.month
df["is_weekend"] = df["day_of_week"].isin([5, 6]).astype(int)

# Rolling window features
df["revenue_7d_avg"] = df.groupby("store_id")["revenue"].transform(
    lambda x: x.rolling(7, min_periods=1).mean()
)

# Lag features
df["revenue_lag_1"] = df.groupby("store_id")["revenue"].shift(1)

# Encoding categorical variables
df = pd.get_dummies(df, columns=["category"], drop_first=True)
```

### Performance Tips

```python
# Use categorical dtype for low-cardinality strings (saves memory)
df["status"] = df["status"].astype("category")

# Use query() for readable filtering
df_filtered = df.query("age > 25 and city == 'Mumbai'")

# Avoid iterrows — use vectorized operations or apply
# BAD
for idx, row in df.iterrows():
    df.loc[idx, "new_col"] = row["a"] * row["b"]

# GOOD
df["new_col"] = df["a"] * df["b"]
```

---

## Common Interview Questions

1. **Q: What's the difference between `.loc` and `.iloc`?**
   > `.loc` is label-based (uses index labels/column names). `.iloc` is integer-position-based (uses integer indices). `df.loc[5]` returns the row with index label 5. `df.iloc[5]` returns the 6th row regardless of index.

2. **Q: How do you handle a DataFrame with 10GB of data that doesn't fit in memory?**
   > Options: (1) Use `pd.read_csv(..., chunksize=10000)` to process in chunks. (2) Use `dtype` optimization to reduce memory. (3) Use Dask or Polars for out-of-core processing. (4) Filter/aggregate in SQL before loading.

3. **Q: Explain the difference between `apply`, `map`, and `applymap`.**
   > `map` works on a Series (element-wise). `apply` works on a Series or DataFrame (can operate on rows/columns). `applymap` works element-wise on a DataFrame (deprecated in newer pandas — use `map` on DataFrame instead).

4. **Q: What's a MultiIndex and when would you use it?**
   > A hierarchical index that allows multiple levels of indexing. Useful for panel data (e.g., user + date), pivot tables, and grouped time-series data.

---

## Try It Yourself

1. Download the Titanic dataset. Clean it: handle missing values, encode categoricals, create 3 new features.
2. Implement standardization (zero mean, unit variance) in pure NumPy — then with pandas.
3. Write a `groupby` pipeline to compute: retention rate by cohort (month of first purchase).

---

## Resources

- 📖 [NumPy User Guide](https://numpy.org/doc/stable/user/index.html)
- 📖 [Pandas User Guide](https://pandas.pydata.org/docs/user_guide/index.html)
- 📺 [Corey Schafer — Pandas Tutorials](https://www.youtube.com/playlist?list=PL-osiE80TeTsWmV9i9c58mdDCSskIFdDS)
]]>
