# 🤖 Day 7 — Large Language Models (LLMs): GPT, LLaMA & the Rise of GenAI

**Date:** 2026-03-14  
**Topic:** LLMs — The Technology Behind ChatGPT  
**Papers:** [GPT-3 (2020)](https://arxiv.org/abs/2005.14165) · [LLaMA (2023)](https://arxiv.org/abs/2302.13971)  
**Level:** 🟡 Intermediate

---

## What Is a Large Language Model?

A Large Language Model is a **Transformer trained on massive amounts of text** to predict the next word (token). That's it. But this simple objective, scaled to billions of parameters and trillions of tokens, produces a model that can:

- Write code, essays, poems
- Summarize, translate, explain
- Answer questions, reason step-by-step
- Generate SQL, debug errors, pass exams

The key realization: **predicting the next word requires understanding language, facts, reasoning, and context**.

---

## How LLMs are Built

### Step 1 — Pre-training
Train a decoder-only Transformer on internet-scale text using **next-token prediction**:

```
Input:  "The capital of France is"
Target: "Paris"
```

The model sees the input tokens and learns to predict each next token. Trained on trillions of tokens from books, web pages, code, scientific papers.

### Step 2 — Instruction Fine-Tuning (SFT)
Fine-tune on high-quality (prompt, response) pairs so the model follows instructions, not just completes text.

### Step 3 — RLHF (Reinforcement Learning from Human Feedback)
Human raters rank model responses. A **reward model** is trained on these rankings. The LLM is then fine-tuned with RL (PPO) to maximize the reward — making it helpful, harmless, and honest.

```
Pre-trained LLM → SFT → Reward model training → RLHF → ChatGPT / Claude
```

---

## Key Architecture Choices (Decoder-only Transformer)

| Feature | Details |
|---|---|
| **Causal attention** | Each token only attends to previous tokens |
| **Rotary positional embeddings (RoPE)** | Better for long contexts (used in LLaMA) |
| **Grouped Query Attention (GQA)** | Reduces memory, faster inference |
| **RMSNorm** | Faster than LayerNorm |
| **SwiGLU activation** | Better than ReLU for LLMs |

---

## Scaling Laws

Scale → Better models. This is quantified by Chinchilla scaling laws:

> **Optimal model**: For a given compute budget, train a model with ~equal parameter count and token count ratio.

| Model | Params | Tokens trained |
|---|---|---|
| GPT-3 | 175B | 300B |
| LLaMA-2 | 70B | 2T |
| Chinchilla | 70B | 1.4T |

More data often beats more parameters.

---

## Major LLMs

| Model | Org | Params | Open? | Notes |
|---|---|---|---|---|
| **GPT-4** | OpenAI | ~1.8T (MoE) | ❌ | Powers ChatGPT |
| **Claude 3.5** | Anthropic | Unknown | ❌ | Strong reasoning |
| **Gemini Ultra** | Google | Unknown | ❌ | Multimodal |
| **LLaMA 3.1** | Meta | 8B–405B | ✅ | Best open-source |
| **Mistral** | Mistral AI | 7B–141B | ✅ | Efficient, very capable |
| **DeepSeek-R1** | DeepSeek | 671B | ✅ | Reasoning via RL |
| **Qwen 2.5** | Alibaba | 0.5B–72B | ✅ | Multilingual |

---

## Emergent Abilities

At sufficient scale, LLMs develop capabilities that weren't explicitly trained:
- **Few-shot learning** — solve tasks from a few examples in the prompt
- **Chain-of-thought reasoning** — think step-by-step
- **Code generation** — write functional code
- **Instruction following** — understand complex multi-step instructions

---

## Key Concepts

| Term | Meaning |
|---|---|
| **Token** | Basic unit of text (word or sub-word) |
| **Context window** | Max tokens the model can process at once |
| **Temperature** | Controls randomness of generation |
| **Top-p / Top-k** | Sampling strategies for next token |
| **Prompt engineering** | Crafting inputs to steer model behavior |
| **RAG** | Augment LLM with retrieved external documents |
| **Fine-tuning** | Further training on domain-specific data |
| **LoRA** | Efficient fine-tuning with low-rank adapters |

---

## 🔗 Resources
- [GPT-3 Paper](https://arxiv.org/abs/2005.14165)
- [LLaMA 2 Paper](https://arxiv.org/abs/2307.09288)
- [Andrej Karpathy: Build GPT from scratch (video)](https://www.youtube.com/watch?v=kCc8FmEb1nY)
- [HuggingFace LLM Course](https://huggingface.co/learn/llm-course/)

---

*You've completed the 7-day Deep Learning foundations series! 🎉*
