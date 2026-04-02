# 🎯 Day 9 — RLHF: Reinforcement Learning from Human Feedback

**Date:** 2026-04-02  
**Topic:** RLHF — Aligning LLMs with Human Preferences  
**Papers:** [InstructGPT (2022)](https://arxiv.org/abs/2203.02155) · [Training Language Models to Follow Instructions](https://arxiv.org/abs/2203.02155) · [DPO (2023)](https://arxiv.org/abs/2305.18290)  
**Level:** 🔴 Advanced

---

## The Problem: LLMs Are Powerful but Misaligned

Pre-trained LLMs are impressive text predictors, but they have serious alignment issues:

- **Toxicity** — Models can generate harmful, biased, or offensive content
- **Unhelpfulness** — They may produce technically correct but useless responses
- **Instruction ignoring** — Pre-trained models aren't naturally good at following instructions
- **Sycophancy** — Models may agree with users instead of being truthful

> **The core question**: How do you make an LLM *helpful, harmless, and honest* — not just fluent?

---

## The Three-Stage RLHF Pipeline

RLHF was the key innovation behind ChatGPT and InstructGPT. It works in three stages:

```
Stage 1: Supervised Fine-Tuning (SFT)
    Pre-trained LLM → Fine-tune on high-quality (prompt, response) pairs

Stage 2: Reward Model Training
    Collect human rankings of model outputs → Train a reward model

Stage 3: RL Optimization (PPO)
    Use the reward model to optimize the LLM via Proximal Policy Optimization
```

---

## Stage 1: Supervised Fine-Tuning (SFT)

Start with a pre-trained base model (e.g., GPT-3) and fine-tune it on a curated dataset of high-quality demonstrations.

| Aspect | Details |
|---|---|
| **Data source** | Human labelers write ideal responses to prompts |
| **Dataset size** | ~13,000 demonstrations (InstructGPT) |
| **Purpose** | Teach the model *what a good response looks like* |
| **Output** | SFT model — better at following instructions, but still imperfect |

> The SFT model is a starting point. It's better than the base model but still needs alignment.

---

## Stage 2: Reward Model Training

The reward model learns to score how "good" a response is, based on human preferences.

### How It Works

1. **Generate**: Given a prompt, sample K responses from the SFT model
2. **Rank**: Human labelers rank responses from best to worst
3. **Train**: Train a reward model to predict human preferences

```
Prompt: "Explain quantum computing simply"

Response A: [Technical jargon, no examples]     → Score: 2.1
Response B: [Clear analogy, step-by-step]        → Score: 8.7
Response C: [Partially correct, rambling]        → Score: 4.3

Reward Model learns: B > C > A
```

### The Reward Model Architecture

| Component | Details |
|---|---|
| **Base** | Same architecture as the LLM (e.g., GPT-3 6B) |
| **Output** | Single scalar reward score |
| **Training objective** | Bradley-Terry pairwise ranking loss |
| **Data** | ~33,000 comparison pairs (InstructGPT) |

### The Loss Function

For a pair of responses (yᵤ, yₗ) where yᵤ is preferred:

```
L(θ) = -log(σ(rθ(x, yᵤ) - rθ(x, yₗ)))
```

This pushes the reward model to assign higher scores to human-preferred responses.

---

## Stage 3: PPO Optimization

Use the reward model as a signal to fine-tune the LLM with Proximal Policy Optimization (PPO).

### The RL Setup

| RL Concept | RLHF Mapping |
|---|---|
| **Environment** | Token-by-token text generation |
| **State** | Prompt + tokens generated so far |
| **Action** | Choosing the next token |
| **Policy** | The LLM being optimized |
| **Reward** | Score from the reward model (given at end of sequence) |

### The Objective Function

```
maximize  E[R(x, y)] - β · KL(π_RL ‖ π_SFT)
```

Where:
- **R(x, y)** — Reward model score for prompt x and response y
- **KL(π_RL ‖ π_SFT)** — KL divergence penalty to prevent the model from drifting too far from the SFT model
- **β** — Controls the strength of the KL penalty

> **Why the KL penalty?** Without it, the model could "hack" the reward model by generating degenerate text that scores high but is nonsensical. The KL constraint keeps outputs natural.

---

## Key Results (InstructGPT)

### Human Preference

| Model | Win Rate vs. GPT-3 175B |
|---|---|
| SFT (baseline) | ~60% |
| InstructGPT 1.3B (RLHF) | **~85%** |
| InstructGPT 175B (RLHF) | **~93%** |

> A 1.3B parameter InstructGPT model was preferred over the 175B GPT-3 — showing that **alignment can matter more than raw scale**.

### Safety Improvements

| Metric | GPT-3 | InstructGPT |
|---|---|---|
| Truthful (TruthfulQA) | 22% | **34%** |
| Non-toxic generations | 73% | **89%** |
| Hallucination rate | High | Reduced |

---

## Beyond PPO: Direct Preference Optimization (DPO)

DPO (Rafailov et al., 2023) simplifies RLHF by eliminating the reward model entirely:

### The Key Insight

> The optimal policy under the RLHF objective has a **closed-form solution** in terms of the reward function. You can directly optimize the policy without training a separate reward model.

### DPO vs. RLHF

| Aspect | RLHF (PPO) | DPO |
|---|---|---|
| **Pipeline** | 3 stages (SFT → RM → PPO) | 2 stages (SFT → DPO) |
| **Reward model** | Explicit, separately trained | Implicit (derived from policy) |
| **Training stability** | Tricky (PPO hyperparameters) | Stable (standard cross-entropy) |
| **Compute** | Higher (RL loop + reward inference) | Lower (single optimization) |
| **Performance** | Strong | Comparable or better |

### DPO Loss Function

```
L_DPO(θ) = -log σ(β · (log π_θ(yᵤ|x)/π_ref(yᵤ|x) - log π_θ(yₗ|x)/π_ref(yₗ|x)))
```

Where yᵤ is the preferred response and yₗ is the dispreferred one.

---

## The Alignment Landscape (2024–2025)

| Method | Key Idea |
|---|---|
| **RLHF (PPO)** | Train reward model + PPO optimization |
| **DPO** | Direct policy optimization from preferences |
| **KTO** | Optimize from binary (good/bad) feedback, no pairs needed |
| **ORPO** | Combine SFT + preference optimization in one step |
| **Constitutional AI (CAI)** | LLM self-critiques using a constitution of principles |
| **RLAIF** | Replace human feedback with AI feedback |
| **SteerLM** | Attribute-conditioned generation for fine-grained control |

---

## Why RLHF Matters

1. **ChatGPT's secret sauce** — RLHF is what made GPT-3.5 conversational and helpful
2. **Alignment is the bottleneck** — Pre-training scales with compute; alignment scales with *human values*
3. **Safety-critical** — Without alignment, powerful LLMs can be dangerous
4. **Ongoing research** — The field is rapidly evolving toward more efficient, scalable alignment methods

---

## Practical Considerations

### Common Challenges

| Challenge | Description |
|---|---|
| **Reward hacking** | Model exploits reward model without improving quality |
| **Human labeler disagreement** | Preferences are subjective and noisy |
| **Distribution shift** | Policy drifts from training distribution |
| **Scaling human feedback** | Human labeling is expensive and slow |
| **Overoptimization** | Too much RL training degrades generation quality |

### Popular Frameworks

```python
# Using TRL (Transformer Reinforcement Learning) by HuggingFace
from trl import PPOTrainer, PPOConfig, AutoModelForCausalLMWithValueHead

# Configure PPO
ppo_config = PPOConfig(
    model_name="gpt2",
    learning_rate=1.41e-5,
    batch_size=256,
    mini_batch_size=16,
)

# Initialize model with value head for RL
model = AutoModelForCausalLMWithValueHead.from_pretrained("gpt2")

# Train with PPO
ppo_trainer = PPOTrainer(ppo_config, model, tokenizer=tokenizer)
```

---

## 🔗 Resources
- [InstructGPT Paper (Ouyang et al., 2022)](https://arxiv.org/abs/2203.02155)
- [DPO Paper (Rafailov et al., 2023)](https://arxiv.org/abs/2305.18290)
- [Anthropic RLHF Paper](https://arxiv.org/abs/2204.05862)
- [HuggingFace TRL Library](https://github.com/huggingface/trl)
- [Chip Huyen: RLHF Explained](https://huyenchip.com/2023/05/02/rlhf.html)

---

*Day 9 of the AI/ML Foundations series — RLHF is the bridge between a language model and an AI assistant. Without alignment, intelligence is just autocomplete. 🧭*
