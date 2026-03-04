<![CDATA[# Case Study: Spam Classifier

> **Interview relevance:** Classic NLP + classification problem. Tests feature engineering, model selection, and deployment thinking.

---

## Problem Statement

Build a classifier that labels emails as spam or not-spam (ham).

## Pipeline

### 1. Data Preprocessing

```python
import re
import pandas as pd

def clean_text(text):
    text = text.lower()
    text = re.sub(r'<[^>]+>', '', text)       # Remove HTML tags
    text = re.sub(r'http\S+', 'URL', text)    # Replace URLs
    text = re.sub(r'\d+', 'NUM', text)        # Replace numbers
    text = re.sub(r'[^\w\s]', '', text)       # Remove punctuation
    return text.strip()
```

### 2. Feature Engineering

```python
from sklearn.feature_extraction.text import TfidfVectorizer

tfidf = TfidfVectorizer(max_features=5000, ngram_range=(1, 2), stop_words='english')
X = tfidf.fit_transform(df['cleaned_text'])
```

### 3. Model Training

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import cross_val_score

model = LogisticRegression(C=1.0, max_iter=1000)
scores = cross_val_score(model, X, y, cv=5, scoring='f1')
print(f"CV F1: {scores.mean():.4f} ± {scores.std():.4f}")
```

### 4. Evaluation

- **Primary metric:** F1-score (balance precision and recall)
- **Precision matters:** Don't want to block legitimate emails
- **Recall matters:** Don't want spam reaching the inbox

### 5. Deployment Considerations

- TF-IDF vocabulary must be saved with the model (`joblib.dump`)
- Input validation: handle empty strings, very long texts 
- Logging: track predictions for monitoring drift
- Latency target: < 50ms per prediction

## Interview Questions

1. Why TF-IDF over bag of words?
2. How would you handle concept drift (new spam patterns)?
3. Would you use deep learning here? When is it worth it?
4. How do you set the classification threshold?
]]>
