# Insurance Claim Predictor

Full MLOps: Airflow → MLflow → Docker → FastAPI → monitoring.

---

## Problem Statement

Claims processing takes 5-7 days. Manual review is inconsistent and doesn't scale. Need automated first-pass assessment that flags high-risk claims for human review.

---

## Architecture

```
Airflow DAG → Data Ingestion → Feature Engineering → Training → MLflow Registry → FastAPI → Monitoring
```

---

## Approach + Why

| Decision | Choice | Why |
|----------|--------|-----|
| **Orchestration** | Airflow over cron | Visual DAGs, retry logic, monitoring |
| **Tracking** | MLflow over W&B | Open-source, self-hosted, model registry |
| **Container** | Docker | Reproducibility, deployment consistency |
| **API** | FastAPI | Async, automatic docs, type safety |

---

## Metrics Target

| Metric | Target | Why |
|--------|--------|-----|
| AUC-ROC | > 0.65 | Baseline for production viability |
| API Latency | p99 < 200ms | User experience |

---

## What I Learned

1. **The hardest part isn't the model — it's the data pipeline**
2. **Schema drift breaks everything** — Need schema validation at ingestion
3. **Monitoring matters more than accuracy** — Models degrade silently without drift detection

---

## Status

🚧 In development
