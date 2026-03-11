# ⚡ Day 4 — Transformers: Attention Is All You Need

**Date:** 2026-03-11  
**Topic:** Transformers — The Architecture Powering Modern AI  
**Paper:** [Vaswani et al., 2017](https://arxiv.org/abs/1706.03762)  
**Level:** 🟡 Intermediate

---

## Why Transformers Changed Everything

Before 2017, NLP used RNNs — but they had two big problems:
1. **Sequential processing** — can't parallelize, train slowly
2. **Vanishing gradients** — forget distant context

The Transformer (2017) threw out recurrence entirely and replaced it with **self-attention** — letting every word look at every other word simultaneously. This single idea powers GPT, BERT, LLaMA, Stable Diffusion, and ViT.

---

## Self-Attention: The Core Idea

For a sentence like *"The animal didn't cross the street because it was too tired"* — what does "it" refer to?

Self-attention lets each word compute how relevant every other word is to itself, then build a representation that **incorporates context from the whole sequence** at once.

Each word is represented as three vectors:
- **Q (Query)** — "what am I looking for?"
- **K (Key)** — "what do I contain?"
- **V (Value)** — "what do I offer if selected?"

```
Attention(Q, K, V) = softmax(QKᵀ / √d) · V
```

- `QKᵀ` → similarity scores between all pairs of words
- `/ √d` → scaling to prevent large dot products
- `softmax` → convert to weights that sum to 1
- `× V` → weighted sum of values

---

## Multi-Head Attention

Instead of one attention computation, use **h parallel heads** — each learning to attend to different aspects (syntax, coreference, proximity):

```
MultiHead(Q,K,V) = Concat(head₁, ..., headₕ) · Wₒ
```

---

## The Full Transformer Architecture

```
Input Tokens
    ↓
[Embedding + Positional Encoding]   ← adds position info (no recurrence!)
    ↓
[Multi-Head Self-Attention]         ← each token attends to all others
    ↓
[Add & LayerNorm]                   ← residual connection
    ↓
[Feed-Forward Network]              ← per-position transformation
    ↓
[Add & LayerNorm]
    ↓
(repeat N times)
    ↓
Output
```

**Positional Encoding** is critical — since attention has no notion of order, position info is injected as a sinusoidal signal added to the embeddings.

---

## Encoder vs Decoder

| Component | Used In | Does |
|---|---|---|
| **Encoder** | BERT, ViT | Understands input (bidirectional attention) |
| **Decoder** | GPT, LLaMA | Generates output (masked, causal attention) |
| **Encoder-Decoder** | T5, original Transformer | Translation, summarization |

---

## Why It Won Over RNNs

| Property | RNN | Transformer |
|---|---|---|
| Parallelizable | ❌ Sequential | ✅ Fully parallel |
| Long-range dependencies | ❌ Fades | ✅ Direct attention |
| Training speed | Slow | Fast (on GPUs/TPUs) |
| Scales with compute | Poorly | ✅ Extremely well |

---

## Impact

Every major AI system today uses Transformers:
- **GPT-4** (OpenAI) — decoder-only
- **BERT** (Google) — encoder-only
- **LLaMA** (Meta) — decoder-only, open source
- **Stable Diffusion** — Transformer in the denoising step
- **ViT** — Transformer applied to image patches

---

## 🔗 Resources
- [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) — best visual explanation
- [Attention Is All You Need (paper)](https://arxiv.org/abs/1706.03762)
- [Andrej Karpathy: nanoGPT — build GPT from scratch](https://github.com/karpathy/nanoGPT)

---

*Next up → Day 5: GANs — The Generator vs Discriminator*
