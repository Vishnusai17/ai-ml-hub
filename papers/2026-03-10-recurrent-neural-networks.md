# 🔄 Day 3 — Recurrent Neural Networks (RNNs) & LSTMs

**Date:** 2026-03-10  
**Topic:** RNNs & LSTMs — Memory for Sequences  
**Level:** 🟡 Intermediate

---

## Why Sequences Need a Different Architecture

CNNs are great for images — but what about text, speech, or time-series data? These are **sequences** where the order matters:

- *"The cat sat on the mat"* — understanding "it" requires knowing "cat" came before
- Stock prices — today's price depends on yesterday's
- Speech — sounds form words over time

Standard networks process each input independently. RNNs process inputs **one at a time** while maintaining a hidden state — a kind of **memory** of what came before.

---

## How an RNN Works

At each time step, an RNN takes:
1. The current input `xₜ`
2. The previous hidden state `hₜ₋₁`

And produces:
1. A new hidden state `hₜ` (updated memory)
2. An output `yₜ`

```
x₁ → [RNN cell] → h₁ → [RNN cell] → h₂ → [RNN cell] → h₃
         ↓                   ↓                   ↓
         y₁                  y₂                  y₃
```

The same cell (same weights) is used at every time step — this is called **weight sharing across time**.

```python
hₜ = tanh(Wₓ · xₜ + Wₕ · hₜ₋₁ + b)
```

---

## The Problem: Vanishing Gradients

Training RNNs with backpropagation requires gradients to flow backward through many time steps. For long sequences, these gradients **shrink exponentially** — the model forgets early parts of the sequence.

This is the **vanishing gradient problem** — and it's why plain RNNs struggle with long-term dependencies.

---

## LSTM: Long Short-Term Memory

LSTMs (1997, Hochreiter & Schmidhuber) solve this with a **cell state** — a highway that carries information across many time steps, protected by three **gates**:

| Gate | Purpose |
|---|---|
| **Forget gate** | Decides what to erase from memory |
| **Input gate** | Decides what new info to add |
| **Output gate** | Decides what to output from memory |

```
Cell state (long-term memory):  ──────────────────────────────→
                                 ↑ forget  ↑ input  ↓ output
Hidden state (short-term):      [LSTM] → [LSTM] → [LSTM]
```

The key insight: cell state updates are **additive** (not multiplicative), so gradients don't vanish over long distances.

---

## GRU: Gated Recurrent Unit

A simpler version of LSTM — combines the forget and input gates into a single **update gate**. Fewer parameters, often performs comparably to LSTM.

---

## Types of RNN Architectures

| Type | Input→Output | Use Case |
|---|---|---|
| **One-to-Many** | Single → Sequence | Image captioning |
| **Many-to-One** | Sequence → Single | Sentiment analysis |
| **Many-to-Many (same)** | Sequence → Sequence | POS tagging |
| **Many-to-Many (diff)** | Sequence → Sequence | Machine translation |

---

## Where RNNs Are Still Used

RNNs have largely been replaced by Transformers for NLP — but they still shine in:
- **Time-series forecasting** (structured temporal data)
- **On-device / low-latency** applications (smaller footprint)
- **Audio processing** (speech recognition edge cases)

---

## Key Terms

| Term | Meaning |
|---|---|
| **Hidden state** | The network's memory of previous inputs |
| **Cell state** | LSTM's long-term memory highway |
| **Vanishing gradient** | Gradients shrink to zero across long sequences |
| **Backprop Through Time (BPTT)** | Backprop unrolled across time steps |
| **Bidirectional RNN** | Processes sequence forward AND backward |

---

## 🔗 Resources
- [Colah's Blog: Understanding LSTMs](https://colah.github.io/posts/2015-08-Understanding-LSTMs/)
- [Andrej Karpathy: The Unreasonable Effectiveness of RNNs](http://karpathy.github.io/2015/05/21/rnn-effectiveness/)

---

*Next up → Day 4: Transformers — Attention Is All You Need*
