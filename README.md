# ML Systems

End-to-end ML systems built after foundational learning. Each project demonstrates production-grade depth: evaluation, deployment, monitoring, and reproducibility.

> These systems build on the 30+ experiments in [ml-engineering-lab](https://github.com/neonite-rc/ml-engineering-lab).

## Systems

| System | What It Does | Stack | Status |
|--------|-------------|-------|--------|
| [`risk-score-pipeline`](risk-score-pipeline/) | SQL feature engineering → XGBoost → FastAPI | PostgreSQL, SQL, XGBoost, FastAPI | 🚧 In development |
| [`domain-transformer-nano`](domain-transformer-nano/) | GPT-2 from scratch, trained on domain corpus | PyTorch, WandB | 🚧 In development |
| [`enterprise-qa-assistant`](enterprise-qa-assistant/) | QLoRA Mistral + evaluated RAG + Streamlit | PEFT, ChromaDB, Streamlit | 🚧 In development |
| [`insurance-claim-predictor`](insurance-claim-predictor/) | Full MLOps: Airflow → MLflow → Docker → API | Airflow, MLflow, Docker, FastAPI | 🚧 In development |

## Philosophy
One deployed system with metrics beats six tutorial notebooks. These repos prove I can build deliberately, evaluate rigorously, and ship.
