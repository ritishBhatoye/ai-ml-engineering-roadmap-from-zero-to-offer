<![CDATA[# Flask & FastAPI for ML Model Serving

> **Interview weight:** ⭐⭐⭐ — Demonstrates you can ship models, not just train them.

---

## FastAPI (Recommended)

```python
# app.py
from fastapi import FastAPI
from pydantic import BaseModel
import joblib
import numpy as np

app = FastAPI(title="ML Prediction API")

# Load model at startup
model = joblib.load("model.pkl")
scaler = joblib.load("scaler.pkl")

class PredictionRequest(BaseModel):
    features: list[float]

class PredictionResponse(BaseModel):
    prediction: int
    probability: float

@app.get("/health")
def health():
    return {"status": "healthy"}

@app.post("/predict", response_model=PredictionResponse)
def predict(request: PredictionRequest):
    X = np.array(request.features).reshape(1, -1)
    X_scaled = scaler.transform(X)
    prediction = int(model.predict(X_scaled)[0])
    probability = float(model.predict_proba(X_scaled)[0][1])
    return PredictionResponse(prediction=prediction, probability=probability)
```

### Run It

```bash
pip install fastapi uvicorn
uvicorn app:app --host 0.0.0.0 --port 8000 --reload
# Test: curl -X POST http://localhost:8000/predict \
#   -H "Content-Type: application/json" \
#   -d '{"features": [1.5, 2.3, 0.7, 1.2]}'
```

### Why FastAPI over Flask?

| Feature | Flask | FastAPI |
|---|---|---|
| Async support | No (needs extensions) | Built-in |
| Auto documentation | No | Swagger UI at `/docs` |
| Input validation | Manual | Pydantic models |
| Performance | Good | 2-3x faster |
| Type hints | Optional | Core feature |

---

## Best Practices

1. **Load model once** at startup (not per request)
2. **Input validation** with Pydantic (catch bad inputs early)
3. **Health endpoint** for load balancers and monitoring
4. **Logging** — log every prediction for debugging and monitoring
5. **Error handling** — return meaningful error messages
6. **Versioning** — `/v1/predict`, `/v2/predict`

---

## Resources

- 📖 [FastAPI Documentation](https://fastapi.tianjolo.com/)
- 📖 [Deploying ML Models with FastAPI (tutorial)](https://testdriven.io/blog/fastapi-machine-learning/)
]]>
