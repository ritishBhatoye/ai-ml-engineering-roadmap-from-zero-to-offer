# Project 4: End-to-End Deployed ML Model

## Objective

Build, containerize, and deploy an ML model as a REST API. This is the project that separates you from 90% of other candidates.

**Why this matters:** Most candidates can train models. Few can deploy them. This shows you understand the full ML lifecycle.

---

## Suggested Problem

**Spam Email Classifier** — Text classification is clean, demonstrable, and interview-friendly.

Alternative problems:
- Sentiment Analysis API
- Customer Churn Prediction API
- Housing Price Prediction API

---

## Deliverables Checklist

### Model
- [ ] Train TF-IDF + Logistic Regression (baseline)
- [ ] Or: Fine-tune DistilBERT for text classification
- [ ] Save model and vectorizer with `joblib` or `pickle`

### API
- [ ] FastAPI app with `/predict` endpoint
- [ ] Pydantic input validation
- [ ] `/health` endpoint for health checks
- [ ] Proper error handling and status codes
- [ ] Auto-generated docs at `/docs`

### Containerization
- [ ] Dockerfile with multi-stage build
- [ ] docker-compose.yml for one-command startup
- [ ] Requirements.txt with pinned versions

### Testing & CI/CD
- [ ] Unit tests with pytest
- [ ] GitHub Actions: lint → test → build Docker image
- [ ] Test the containerized API

### Documentation
- [ ] API documentation with curl examples
- [ ] Architecture diagram
- [ ] Clear README with how to run

---

## Assessment Criteria

| Criterion | Weight | What Interviewers Look For |
|-----------|--------|---------------------------|
| Model Quality | 15% | Reasonable accuracy, proper evaluation |
| API Design | 20% | Clean endpoints, validation, error handling |
| Docker | 15% | Proper Dockerfile, optimized image size |
| CI/CD | 15% | Working GitHub Actions pipeline |
| Testing | 15% | Unit tests with reasonable coverage |
| Documentation | 10% | Clear API docs, run instructions |
| Code Quality | 10% | Modular, type hints, clean structure |

---

## Suggested Structure

```
04-deployed-model/
├── app/
│   ├── __init__.py
│   ├── main.py                # FastAPI app
│   ├── model.py               # Model loading & prediction
│   └── schemas.py             # Pydantic models
├── model/
│   ├── model.pkl
│   └── vectorizer.pkl
├── training/
│   └── train.py               # Training script
├── tests/
│   └── test_api.py            # API tests
├── .github/
│   └── workflows/
│       └── ci.yml             # GitHub Actions
├── Dockerfile
├── docker-compose.yml
├── .dockerignore
├── requirements.txt
└── README.md
```

---

## Starter Code

```python
# app/schemas.py
from pydantic import BaseModel, Field

class PredictionRequest(BaseModel):
    text: str = Field(..., min_length=1, max_length=10000)

class PredictionResponse(BaseModel):
    prediction: str
    probability: float
    confidence: str
```

```python
# app/model.py
import joblib
import numpy as np
from pathlib import Path

MODEL_PATH = Path(__file__).parent.parent / "model"

class SpamClassifier:
    def __init__(self):
        self.model = joblib.load(MODEL_PATH / "model.pkl")
        self.vectorizer = joblib.load(MODEL_PATH / "vectorizer.pkl")
    
    def predict(self, text: str) -> dict:
        X = self.vectorizer.transform([text])
        prob = self.model.predict_proba(X)[0]
        pred = self.model.classes_[np.argmax(prob)]
        
        return {
            "prediction": pred,
            "probability": float(max(prob)),
            "confidence": "high" if max(prob) > 0.8 else "medium" if max(prob) > 0.6 else "low"
        }
```

```python
# app/main.py
from fastapi import FastAPI, HTTPException
from app.schemas import PredictionRequest, PredictionResponse
from app.model import SpamClassifier
import logging

app = FastAPI(title="Spam Classifier API", version="1.0.0")
logger = logging.getLogger(__name__)

classifier = SpamClassifier()

@app.get("/health")
def health_check():
    return {"status": "healthy"}

@app.post("/predict", response_model=PredictionResponse)
def predict(request: PredictionRequest):
    try:
        result = classifier.predict(request.text)
        return PredictionResponse(**result)
    except Exception as e:
        logger.error(f"Prediction error: {e}")
        raise HTTPException(status_code=500, detail="Prediction failed")
```

```dockerfile
# Dockerfile
FROM python:3.9-slim as builder

WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

FROM builder as runtime

COPY app/ ./app/
COPY model/ ./model/

EXPOSE 8000

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
```

```yaml
# docker-compose.yml
version: '3.8'

services:
  api:
    build: .
    ports:
      - "8000:8000"
    environment:
      - PYTHONUNBUFFERED=1
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8000/health"]
      interval: 30s
      timeout: 10s
      retries: 3
```

---

## GitHub Actions CI/CD

```yaml
# .github/workflows/ci.yml
name: CI/CD

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.9'
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Run tests
        run: pytest tests/

  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Build Docker image
        run: docker build -t spam-classifier:${{ github.sha }} .
```

---

## Testing the API

```bash
# Build and run
docker-compose up --build

# Test health endpoint
curl http://localhost:8000/health

# Test prediction
curl -X POST http://localhost:8000/predict \
  -H "Content-Type: application/json" \
  -d '{"text": "Congratulations! You won a free prize."}'
```

---

## Bonus Ideas

- Deploy to GCP Cloud Run or AWS EC2
- Add Prometheus metrics endpoint (`/metrics`)
- Add model versioning
- Add a simple HTML frontend

---

## Estimated Time: 20–25 hours
