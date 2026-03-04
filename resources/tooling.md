# ML Engineering Tools & Cheat Sheets

> Curated tools and quick references for ML engineering.

---

## Python & Data Science

### Essential Libraries

| Library | Purpose | Install |
|---------|---------|---------|
| `numpy` | Numerical computing | `pip install numpy` |
| `pandas` | Data manipulation | `pip install pandas` |
| `matplotlib` | Basic plotting | `pip install matplotlib` |
| `seaborn` | Statistical visualization | `pip install seaborn` |
| `scikit-learn` | ML algorithms | `pip install scikit-learn` |
| `xgboost` | Gradient boosting | `pip install xgboost` |
| `lightgbm` | LightGBM | `pip install lightgbm` |
| `catboost` | CatBoost | `pip install catboost` |
| `torch` | Deep learning (PyTorch) | `pip install torch` |
| `tensorflow` | Deep learning (TF) | `pip install tensorflow` |
| `transformers` | HuggingFace | `pip install transformers` |

### Environment Management

```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows

# Install requirements
pip install -r requirements.txt

# Export requirements
pip freeze > requirements.txt
```

---

## NumPy Quick Reference

```python
import numpy as np

# Creation
arr = np.array([1, 2, 3])
zeros = np.zeros((3, 3))
ones = np.ones((2, 4))
arange = np.arange(0, 10, 2)
linspace = np.linspace(0, 1, 5)

# Shapes
arr.shape          # (3,)
arr.reshape(1, 3)  # Reshape
arr.flatten()      # 1D

# Operations
arr.sum(), arr.mean(), arr.std()
arr.max(), arr.min(), arr.argmax()

# Slicing
arr[1:]           # Index 1 onwards
arr[:, 1]         # Column 1
arr[0:2, 0:2]    # Submatrix

# Broadcasting
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
a + b             # Element-wise
a * 2             # Scalar
```

---

## Pandas Quick Reference

```python
import pandas as pd

# Read/Write
df = pd.read_csv('file.csv')
df.to_csv('output.csv', index=False)

# Basic Info
df.shape, df.dtypes, df.columns
df.head(), df.tail()
df.info(), df.describe()

# Selection
df['col']              # Single column
df[['col1', 'col2']]  # Multiple columns
df.iloc[0:5]           # By index
df.loc[df['col'] > 5] # By condition

# Missing Values
df.isnull().sum()
df.dropna()
df.fillna(value)

# GroupBy
df.groupby('col').agg({'val': 'mean'})

# Merge
pd.merge(df1, df2, on='key', how='inner')
```

---

## Scikit-learn Pipeline

```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.ensemble import RandomForestClassifier

# Numeric pipeline
num_pipeline = Pipeline([
    ('scaler', StandardScaler())
])

# Full pipeline
preprocessor = ColumnTransformer([
    ('num', num_pipeline, ['age', 'income']),
    ('cat', OneHotEncoder(), ['city', 'gender'])
])

# Full ML pipeline
ml_pipeline = Pipeline([
    ('preprocessor', preprocessor),
    ('classifier', RandomForestClassifier())
])

# Train
ml_pipeline.fit(X_train, y_train)
predictions = ml_pipeline.predict(X_test)
```

---

## PyTorch Basics

```python
import torch
import torch.nn as nn
import torch.optim as optim

# Tensors
x = torch.randn(32, 10)  # Random
x = torch.zeros(32, 10)   # Zeros
x = torch.tensor([1, 2, 3])

# GPU
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
x = x.to(device)

# Neural Network
class Net(nn.Module):
    def __init__(self):
        super().__init__()
        self.fc1 = nn.Linear(10, 32)
        self.fc2 = nn.Linear(32, 2)
    
    def forward(self, x):
        x = torch.relu(self.fc1(x))
        x = self.fc2(x)
        return x

# Training
model = Net().to(device)
criterion = nn.CrossEntropyLoss()
optimizer = optim.Adam(model.parameters(), lr=0.001)

for epoch in range(100):
    model.train()
    optimizer.zero_grad()
    outputs = model(inputs)
    loss = criterion(outputs, labels)
    loss.backward()
    optimizer.step()
```

---

## FastAPI Quick Start

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float

@app.get("/")
def read_root():
    return {"message": "Hello"}

@app.post("/predict")
def predict(item: Item):
    return {"name": item.name, "price": item.price}

# Run: uvicorn main:app --reload
```

---

## Docker Commands

```bash
# Build
docker build -t myimage .

# Run
docker run -p 8000:8000 myimage

# Compose
docker-compose up --build

# Common
docker ps              # Running containers
docker logs <id>       # View logs
docker exec -it <id> /bin/bash  # Shell access
```

---

## Git Commands

```bash
# Basic
git init
git clone <url>
git add .
git commit -m "message"
git push origin main

# Branching
git branch feature
git checkout feature
git checkout -b feature
git merge feature

# Undo
git checkout -- file     # Discard changes
git reset HEAD file     # Unstage
git reset --soft HEAD~1 # Undo commit
```

---

## IDE Extensions (VS Code)

| Extension | Purpose |
|-----------|---------|
| Python | Language support |
| Jupyter | Notebook support |
| Pylance | Type checking |
| GitLens | Git integration |
| Docker | Container support |
| Prettier | Code formatting |
| Todo Tree | Track TODOs |

---

## Cheat Sheet Resources

| Topic | Resource |
|-------|----------|
| Python | [Python Cheat Sheet](https://www.pythoncheatsheet.org/) |
| Pandas | [Pandas Cheat Sheet](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf) |
| Scikit-learn | [Sklearn Cheat Sheet](https://scikit-learn.org/stable/tutorial/machine_learning_map/) |
| PyTorch | [PyTorch Cheat Sheet](https://pytorch.org/tutorials/beginner/ptcheat.html) |
| SQL | [SQL Cheat Sheet](https://www.sqltutorial.org/sql-cheat-sheet/) |
| Git | [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf) |
| Docker | [Docker Cheat Sheet](https://docs.docker.com/get-started/docker_cheatsheet.pdf) |
