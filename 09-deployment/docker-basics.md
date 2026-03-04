<![CDATA[# Docker Basics for ML Engineers

> **Interview weight:** ⭐⭐⭐ — Shows production deployment awareness.

---

## Why Docker for ML?

"It works on my machine" → Docker ensures it works **everywhere**.

- Packages your code, dependencies, model, and runtime into a single container
- Same environment in development, testing, and production
- Easy to deploy to any cloud provider

---

## Essential Dockerfile for ML

```dockerfile
# Use a slim Python image
FROM python:3.11-slim

# Set working directory
WORKDIR /app

# Install dependencies first (cached if requirements.txt doesn't change)
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code and model
COPY app.py .
COPY model.pkl .
COPY scaler.pkl .

# Expose the API port
EXPOSE 8000

# Health check
HEALTHCHECK --interval=30s --timeout=10s \
  CMD curl -f http://localhost:8000/health || exit 1

# Run the application
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
```

## Docker Commands Cheat Sheet

```bash
# Build the image
docker build -t ml-api:v1 .

# Run the container
docker run -d -p 8000:8000 --name ml-api ml-api:v1

# View logs
docker logs ml-api

# Stop and remove
docker stop ml-api && docker rm ml-api

# List running containers
docker ps
```

## Docker Compose (Multi-Container)

```yaml
# docker-compose.yml
version: "3.8"
services:
  api:
    build: .
    ports:
      - "8000:8000"
    environment:
      - MODEL_PATH=/app/model.pkl
    volumes:
      - ./models:/app/models
    restart: unless-stopped
```

```bash
docker-compose up -d    # Start
docker-compose down     # Stop
```

## Optimization Tips

1. **Use slim/alpine base images** — `python:3.11-slim` not `python:3.11`
2. **Multi-stage builds** — build dependencies in one stage, copy only artifacts to final
3. **Order Dockerfile for caching** — put rarely-changing layers (dependencies) first
4. **Don't copy training data** — only inference code and model weights
5. **Use `.dockerignore`** — exclude `.git`, `__pycache__`, notebooks, datasets

---

## Resources

- 📖 [Docker Official Getting Started](https://docs.docker.com/get-started/)
- 📖 [Docker for Data Science (free guide)](https://docker-curriculum.com/)
]]>
