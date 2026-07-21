# ML Systems

End-to-end ML systems built after foundational learning. Each project demonstrates production-grade depth: evaluation, deployment, monitoring, and reproducibility.

> These systems build on the 30+ experiments in [ml-engineering-lab](https://github.com/neonite-rc/ml-engineering-lab).

---

## Problem Statement

Insurance fraud costs the industry billions annually. Manual review is slow, inconsistent, and doesn't scale. These systems automate risk scoring, claims prediction, and document analysis — turning raw data into actionable decisions.

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        ML Systems Architecture                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐  │
│  │  Data     │───▶│ Feature  │───▶│ Training │───▶│ Registry │  │
│  │  Source   │    │  Store   │    │ Pipeline │    │  (MLflow)│  │
│  └──────────┘    └──────────┘    └──────────┘    └──────────┘  │
│       │                                              │          │
│       ▼                                              ▼          │
│  ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐  │
│  │  Monitor │◀───│   API    │◀───│  Docker  │◀───│  Model   │  │
│  │  (Drift) │    │ (FastAPI)│    │ Container│    │  Export  │  │
│  └──────────┘    └──────────┘    └──────────┘    └──────────┘  │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Systems

### Risk Score Pipeline
SQL feature engineering → XGBoost → FastAPI

**Problem:** Manual risk assessment takes 30 minutes per application. Need sub-second scoring.

**Approach:** Chose XGBoost over neural net — tabular data, interpretability needed for compliance. SQL CTEs for feature engineering because analysts can maintain them.

**Stack:** PostgreSQL, SQL (CTEs, window functions), XGBoost, FastAPI, pytest, Docker

**Metrics Target:**
- AUC-ROC > 0.65
- SQL query < 500ms per 100K rows
- API p99 latency < 200ms

**What I Learned:** Feature stores reduce training-serving skew. Window functions in SQL are more powerful than Pandas for temporal features.

---

### Domain Transformer (Nano)
GPT-2 from scratch, trained on domain corpus

**Problem:** Generic LLMs don't understand insurance terminology. Need domain-specific language model.

**Approach:** Chose GPT-2 architecture over BERT — generative tasks need autoregressive modeling. Trained from scratch (not fine-tuned) to prove understanding of every layer.

**Stack:** PyTorch, tiktoken, WandB, mixed precision training

**Metrics Target:**
- Val perplexity < 30
- Throughput > 50K tokens/sec (T4)

**What I Learned:** Tokenizer choice matters more than model size for domain-specific text. Mixed precision training gives 2x speedup with minimal quality loss.

---

### Enterprise QA Assistant
QLoRA fine-tuned Mistral + evaluated RAG on synthetic company documents

**Problem:** Employees spend 40% of time searching for information across scattered documents.

**Approach:** Chose QLoRA over full fine-tuning — 90% less memory, comparable quality. RAG over pure generation because answers must be grounded in actual documents.

**Stack:** Mistral-7B, PEFT (QLoRA), ChromaDB, sentence-transformers, Streamlit

**Evaluation:**
- Hit rate, MRR, NDCG for retrieval quality
- BLEU, ROUGE for generation quality
- Human judgment for relevance

**What I Learned:** Chunk size dramatically affects retrieval quality. 512 tokens with 50 token overlap worked best for our document types.

---

### Insurance Claim Predictor
Full MLOps: Airflow → MLflow → Docker → FastAPI → monitoring

**Problem:** Claims processing takes 5-7 days. Need automated first-pass assessment.

**Approach:** Full MLOps pipeline because this is a real production system, not a notebook experiment. Airflow for orchestration, MLflow for tracking, Docker for reproducibility.

**Stack:** Airflow, MLflow, PostgreSQL, XGBoost, FastAPI, Docker, GitHub Actions

**Metrics Target:**
- AUC-ROC > 0.65
- API p99 latency < 200ms

**What I Learned:** The hardest part isn't the model — it's the data pipeline. Schema drift breaks everything. Monitoring matters more than accuracy.

---

## What I Learned (Overall)

1. **Feature stores reduce training-serving skew** — same features in training and production
2. **Interpretability matters for compliance** — black-box models don't pass regulatory review
3. **The hardest part is data, not models** — 80% of effort is data cleaning and feature engineering
4. **Monitoring is not optional** — models degrade silently without drift detection
5. **Docker is non-negotiable** — "works on my machine" doesn't scale

---

## Infrastructure

- **Containerization:** Docker with multi-stage builds
- **Orchestration:** Airflow for pipeline scheduling
- **Tracking:** MLflow for experiment logging and model registry
- **Deployment:** FastAPI with health checks
- **CI/CD:** GitHub Actions for automated testing and deployment

---

## Tests

- Unit tests for feature engineering
- Integration tests for API endpoints
- Model performance tests (AUC-ROC thresholds)
- Load tests for latency requirements

---

## Running Locally

```bash
# Clone
git clone https://github.com/neonite-rc/ml-systems.git
cd ml-systems

# Run a specific system
cd risk-score-pipeline
docker-compose up

# Run tests
pytest tests/
```

---

## Future

- [ ] Add drift detection with Evidently AI
- [ ] Implement A/B testing framework
- [ ] Add Kubernetes deployment manifests
- [ ] Cost optimization with spot instances

---

## License

MIT
