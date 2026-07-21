# Risk Score Pipeline

End-to-end insurance risk scoring: complex SQL feature engineering → Python modeling → deployed API.

## Architecture
```
PostgreSQL → SQL CTEs + windows → XGBoost → FastAPI
```

## Stack
PostgreSQL, SQL (CTEs, window functions), XGBoost, FastAPI, pytest, Docker

## Dataset
Porto Seguro Safe Driver Prediction — 595K rows, binary classification

## Metrics Target
- AUC-ROC > 0.65
- SQL query < 500ms per 100K rows

## Status
🚧 In development
