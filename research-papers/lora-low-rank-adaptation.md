# 🔧 LoRA: Low-Rank Adaptation of Large Language Models

**Paper:** [LoRA: Low-Rank Adaptation of Large Language Models (Hu et al., 2021)](https://arxiv.org/abs/2106.09685)  
**Authors:** Edward Hu, Yelong Shen, Phillip Wallis, Zeyuan Allen-Zhu, Yuanzhi Li, Shean Wang, Lu Wang, Weizhu Chen  
**Published:** June 2021 (Microsoft Research)  
**Topic:** Parameter-Efficient Fine-Tuning (PEFT)

---

## 💡 The Problem

Fine-tuning large language models (like GPT-3 with 175B parameters) is:

- **Expensive** — Requires full copies of all model weights per task
- **Slow** — Updating billions of parameters takes massive GPU memory and time
- **Impractical at scale** — Deploying separate 175B-parameter models per task is unsustainable

> If you have 10 tasks, full fine-tuning means storing 10 × 175B = **1.75 trillion parameters**. That's absurd.

---

## 🧠 The Key Insight

> **Hypothesis**: The weight updates during fine-tuning have a **low intrinsic rank**.

In other words, even though the weight matrices are huge (e.g., 12288 × 12288), the *change* that fine-tuning makes to them can be captured by a much smaller matrix.

---

## 🔬 How LoRA Works

### The Math

For a pre-trained weight matrix **W₀** ∈ ℝ^(d×k), LoRA decomposes the update:

```
W = W₀ + ΔW = W₀ + B × A
```

Where:
- **W₀** is frozen (no gradient updates)
- **A** ∈ ℝ^(r×k) — down-projection (randomly initialized)
- **B** ∈ ℝ^(d×r) — up-projection (initialized to zero)
- **r** ≪ min(d, k) — the rank (typically 4, 8, or 16)

### Trainable Parameters Comparison

| Method | Trainable Params (GPT-3 175B) |
|---|---|
| Full fine-tuning | 175,000,000,000 |
| LoRA (r=4) | ~4,700,000 |
| **Reduction** | **~37,000×** |

### What Happens During Training

```
                    ┌──────────┐
                    │  Frozen  │
         x ──────► │   W₀     │ ──────┐
                    └──────────┘       │
                                       ▼
                    ┌────┐  ┌────┐   (+)──► output
         x ──────► │ A  │─►│ B  │ ────┘
                    └────┘  └────┘
                    (r×k)   (d×r)
                    
                    Trainable LoRA
                    adapters
```

The forward pass computes: **h = W₀x + BAx**

At inference, you can **merge** the LoRA weights back: **W = W₀ + BA**, adding **zero latency**.

---

## 📊 Key Results

### Performance  
LoRA matches or exceeds full fine-tuning on multiple benchmarks:

| Model | Method | WikiSQL Acc | MNLI Acc | SAMSum R-L |
|---|---|---|---|---|
| GPT-3 175B | Full FT | 73.8 | 89.5 | 52.0 |
| GPT-3 175B | LoRA | **73.4** | **91.7** | **53.8** |

### Efficiency
- **Memory**: Up to 2/3 reduction in GPU memory during training
- **Storage**: Each task needs only ~35 MB instead of ~350 GB
- **Speed**: 25% faster training than full fine-tuning
- **No inference latency**: Merge weights at deployment time

---

## 🎯 Where to Apply LoRA

The paper applies LoRA to the **attention weight matrices** (Wq, Wk, Wv, Wo) in each Transformer layer.

| Target Matrices | Performance |
|---|---|
| Wq only | Good |
| Wq + Wv | Better |
| Wq + Wk + Wv + Wo | Best |

> **Finding**: Adapting more weight matrices with a smaller rank is better than adapting fewer matrices with a larger rank (given the same parameter budget).

---

## 🔄 LoRA Variants and Extensions

| Variant | Improvement |
|---|---|
| **QLoRA (2023)** | Quantize base model to 4-bit + LoRA → fine-tune 65B models on a single 48GB GPU |
| **LoRA+ (2024)** | Use different learning rates for A and B matrices |
| **DoRA (2024)** | Decompose weight into magnitude and direction, apply LoRA to direction only |
| **AdaLoRA (2023)** | Adaptively allocate rank budget across layers |
| **rsLoRA (2024)** | Better scaling factor for higher ranks |

---

## 🛠️ Practical Usage

LoRA is supported in all major frameworks:

```python
# Using HuggingFace PEFT
from peft import LoraConfig, get_peft_model

config = LoraConfig(
    r=16,                          # Rank
    lora_alpha=32,                 # Scaling factor
    target_modules=["q_proj", "v_proj"],  # Which layers
    lora_dropout=0.05,
    bias="none",
    task_type="CAUSAL_LM"
)

model = get_peft_model(base_model, config)
model.print_trainable_parameters()
# trainable params: 4,194,304 || all params: 6,742,609,920 || trainable%: 0.0622
```

---

## 🎓 Why This Paper Matters

1. **Democratized fine-tuning** — Anyone with a single GPU can fine-tune large models
2. **Enabled the open-source LLM ecosystem** — QLoRA + LoRA made it practical to fine-tune LLaMA, Mistral, etc.
3. **Task-specific adaptation at scale** — Swap LoRA adapters without loading separate model copies
4. **Foundation for PEFT research** — Sparked an entire subfield of parameter-efficient methods

---

## 🔗 Resources
- [Original Paper](https://arxiv.org/abs/2106.09685)
- [HuggingFace PEFT Library](https://github.com/huggingface/peft)
- [QLoRA Paper](https://arxiv.org/abs/2305.14314)
- [Sebastian Raschka: LoRA Explained](https://magazine.sebastianraschka.com/p/lora-and-dora-from-scratch)

---

*LoRA proved that you don't need to move mountains to adapt them — a small, low-rank nudge is all it takes. 🏔️*
