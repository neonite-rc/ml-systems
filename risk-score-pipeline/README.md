# Risk Score Pipeline

End-to-end insurance risk scoring: complex SQL feature engineering → Python modeling → deployed API.

---

## Problem Statement

Manual risk assessment takes 30 minutes per application. Underwriters need sub-second scoring to handle volume without sacrificing accuracy.

---

## Architecture

```
PostgreSQL → SQL CTEs + window functions → XGBoost → FastAPI → Docker
```

---

## Approach + Why

| Decision | Choice | Why |
|----------|--------|-----|
| **Model** | XGBoost over neural net | Tabular data, interpretability needed for compliance |
| **Features** | SQL CTEs over Pandas | Analysts can maintain, version-controlled |
| **API** | FastAPI over Flask | Async support, automatic OpenAPI docs |
| **Testing** | pytest | Industry standard, good fixtures |

---

## Metrics Target

| Metric | Target | Why |
|--------|--------|-----|
| AUC-ROC | > 0.65 | Baseline for production viability |
| SQL Query Time | < 500ms per 100K rows | Real-time scoring requirement |
| API Latency | p99 < 200ms | User experience |

---

## What I Learned

1. **Window functions in SQL** are more powerful than Pandas for temporal features
2. **Feature stores reduce training-serving skew** — same features in training and production
3. **Interpretability matters** — black-box models don't pass regulatory review

---

## Running Locally

```bash
docker-compose up
```

---

## Status

🚧 In development
