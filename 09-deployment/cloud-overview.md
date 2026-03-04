<![CDATA[# Cloud Overview for ML Engineers

> **Interview weight:** ⭐⭐ — Conceptual awareness is sufficient at intern level.

---

## AWS for ML

| Service | What It Does | When You'd Use It |
|---|---|---|
| **S3** | Object storage (files, datasets, models) | Store training data and model artifacts |
| **EC2** | Virtual machines | Run training jobs or host APIs |
| **SageMaker** | End-to-end ML platform | Training, tuning, deploying models |
| **Lambda** | Serverless functions | Lightweight inference (< 15 min, < 10GB) |
| **ECR** | Docker container registry | Store Docker images for deployment |

## GCP for ML

| Service | What It Does | When You'd Use It |
|---|---|---|
| **GCS** | Object storage | Same as S3 |
| **Compute Engine** | Virtual machines | Same as EC2 |
| **Vertex AI** | ML platform | Training + serving |
| **Cloud Run** | Serverless containers | Deploy Docker containers without managing servers |
| **BigQuery** | Data warehouse | SQL queries on massive datasets |

## Minimal Cloud Deployment

The cheapest way to deploy an ML model:

1. **Containerize** your FastAPI app with Docker
2. **Push** to a container registry (ECR or GCR)
3. **Deploy** to a free/cheap compute service:
   - AWS: EC2 t2.micro (free tier) or Lambda
   - GCP: Cloud Run (generous free tier)

```bash
# Example: Deploy to GCP Cloud Run
gcloud builds submit --tag gcr.io/PROJECT_ID/ml-api
gcloud run deploy ml-api --image gcr.io/PROJECT_ID/ml-api --platform managed
```

## What You Should Know for Interviews

1. The difference between compute (EC2) and serverless (Lambda/Cloud Run)
2. Where to store training data (S3/GCS) and model artifacts
3. Basic cost awareness — GPU instances are expensive, use spot/preemptible
4. How CI/CD pipelines deploy containers to cloud services

---

## Resources

- 📖 [AWS Free Tier](https://aws.amazon.com/free/)
- 📖 [GCP Free Tier](https://cloud.google.com/free)
]]>
