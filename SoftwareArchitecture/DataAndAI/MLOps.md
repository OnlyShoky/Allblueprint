# MLOps (Machine Learning Operations)

**Definition:** The set of practices that aims to deploy and maintain machine learning models in production reliably and efficiently.

## The MLOps Lifecycle

1. **Data Collection & Versioning:** DVC, Pachyderm.
2. **Experiment Tracking:** MLflow, Weights & Biases.
3. **Model Training:** CI/CD for ML (CT - Continuous Training).
4. **Model Registry:** Versioned storage for artifacts.
5. **Deployment:**
   - **Real-time:** REST API (FastAPI, TF Serving).
   - **Batch:** Scheduled jobs (Airflow).
6. **Monitoring:** Drift detection (Data drift, Concept drift).

## Deployment Strategies

### Shadow Deployment
Run new model alongside old one. Only old model serves traffic; new model's predictions are logged for comparison.

### Canary Deployment
Route small % of traffic to new model. Gradually increase if metrics look good.

### A/B Testing
Route traffic to Model A and Model B to compare business metrics (e.g., conversion rate).

## Monitoring Drift
**Data Drift:** Input distribution changes (e.g., users are younger now).
**Concept Drift:** Relationship between input and output changes (e.g., housing prices change due to inflation).
