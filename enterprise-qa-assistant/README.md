# Enterprise QA Assistant

QLoRA fine-tuned Mistral + evaluated RAG on synthetic company documents.

---

## Problem Statement

Employees spend 40% of time searching for information across scattered documents. Policies, procedures, and FAQs are buried in PDFs, wikis, and email threads. Need intelligent search that understands context.

---

## Architecture

```
Documents → Chunking → Embedding → ChromaDB → Retrieval → Mistral (QLoRA) → Answer
```

---

## Approach + Why

| Decision | Choice | Why |
|----------|--------|-----|
| **Fine-tuning** | QLoRA over full | 90% less memory, comparable quality |
| **Retrieval** | RAG over pure generation | Answers must be grounded in actual documents |
| **Embedding** | sentence-transformers | Fast, accurate, well-tested |
| **Vector Store** | ChromaDB over Pinecone | Local, no vendor lock-in |

---

## Evaluation

| Metric | What It Measures |
|--------|------------------|
| Hit Rate | Did we retrieve the right document? |
| MRR | How high is the right document ranked? |
| NDCG | Are relevant documents ranked above irrelevant? |
| BLEU | Does the answer match reference answers? |
| ROUGE | Does the answer capture key information? |

---

## What I Learned

1. **Chunk size dramatically affects retrieval quality** — 512 tokens with 50 overlap worked best
2. **QLoRA is surprisingly effective** — 90% less memory, 95% of full fine-tuning quality
3. **Evaluation matters more than training** — You can't improve what you can't measure

---

## Status

🚧 In development
