# Domain Transformer (Nano)

GPT-2 small from scratch in PyTorch, trained on domain-specific corpus. Not a fork — written independently to prove understanding of every layer.

---

## Problem Statement

Generic LLMs don't understand insurance terminology. "Policyholder," "indemnity," and "subrogation" are rare in general corpora. Need domain-specific language model for accurate document analysis.

---

## Architecture

```
Tokenized Corpus → GPT-2 Architecture → Training Loop → Domain Model
     ↓                    ↓                   ↓              ↓
  tiktoken          Transformer         WandB logging    Model weights
                    Decoder Only        Mixed precision
```

---

## Approach + Why

| Decision | Choice | Why |
|----------|--------|-----|
| **Architecture** | GPT-2 over BERT | Generative tasks need autoregressive modeling |
| **Training** | From scratch over fine-tuning | Prove understanding of every layer |
| **Tokenizer** | tiktoken (BPE) | Fast, well-tested, compatible with OpenAI |

---

## Metrics Target

| Metric | Target | Why |
|--------|--------|-----|
| Val Perplexity | < 30 | Indicates coherent text generation |
| Throughput | > 50K tokens/sec (T4) | Training efficiency |

---

## What I Learned

1. **Tokenizer choice matters more than model size** for domain-specific text
2. **Mixed precision training** gives 2x speedup with minimal quality loss
3. **Learning rate scheduling** is critical — constant LR causes divergence

---

## Status

🚧 In development
