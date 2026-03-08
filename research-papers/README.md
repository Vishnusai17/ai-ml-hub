# 📄 Research Papers

A curated collection of landmark and emerging papers — each with a plain-English summary so you understand the *why*, not just the *what*.

---

## 🏛️ Landmark Papers (Foundational — Must Read)

### Transformers & Attention

#### [Attention Is All You Need (2017)](https://arxiv.org/abs/1706.03762)
**Authors:** Vaswani et al. (Google Brain)  
**Summary:** Introduced the Transformer architecture, replacing RNNs entirely with self-attention. Every modern LLM (GPT, BERT, LLaMA) is built on this foundation.  
**Key idea:** Multi-head self-attention + positional encoding + feed-forward layers  
**Impact:** ⭐⭐⭐⭐⭐ — arguably the most influential ML paper of the decade

---

#### [BERT: Pre-training of Deep Bidirectional Transformers (2018)](https://arxiv.org/abs/1810.04805)
**Authors:** Devlin et al. (Google)  
**Summary:** Showed that a Transformer pre-trained on masked language modeling and next-sentence prediction achieves state-of-the-art on 11 NLP tasks with simple fine-tuning.  
**Key idea:** Bidirectional context via masked language modeling (MLM)  
**Impact:** ⭐⭐⭐⭐⭐

---

### Large Language Models

#### [GPT-3: Language Models are Few-Shot Learners (2020)](https://arxiv.org/abs/2005.14165)
**Authors:** Brown et al. (OpenAI)  
**Summary:** 175B parameter model that can perform tasks with just a few examples in the prompt — no gradient updates. Demonstrated emergent in-context learning at scale.  
**Key idea:** Scale + in-context learning = few-shot generalization  
**Impact:** ⭐⭐⭐⭐⭐

---

#### [LLaMA: Open and Efficient Foundation Language Models (2023)](https://arxiv.org/abs/2302.13971)
**Authors:** Touvron et al. (Meta AI)  
**Summary:** Open-source LLMs from 7B to 65B parameters that match or exceed GPT-3 on many benchmarks. Democratized LLM research.  
**Key idea:** More data + better data quality > simply more parameters  
**Impact:** ⭐⭐⭐⭐⭐

---

### Vision

#### [ViT: An Image is Worth 16x16 Words (2021)](https://arxiv.org/abs/2010.11929)
**Authors:** Dosovitskiy et al. (Google)  
**Summary:** Applied the Transformer directly to image patches, achieving state-of-the-art image classification without convolutions at large scale.  
**Key idea:** Split image into fixed-size patches, treat like tokens  
**Impact:** ⭐⭐⭐⭐⭐

---

#### [CLIP: Learning Transferable Visual Models from Natural Language Supervision (2021)](https://arxiv.org/abs/2103.00020)
**Authors:** Radford et al. (OpenAI)  
**Summary:** Trained a vision-language model on 400M image-text pairs using contrastive learning. Powers DALL-E, GPT-4V, and zero-shot image classification.  
**Key idea:** Match images to their text descriptions via contrastive loss  
**Impact:** ⭐⭐⭐⭐⭐

---

### Generative Models

#### [Denoising Diffusion Probabilistic Models (2020)](https://arxiv.org/abs/2006.11239)
**Authors:** Ho et al.  
**Summary:** Showed that iteratively denoising random noise produces high-quality images. Forms the foundation of Stable Diffusion, DALL-E 2, and Midjourney.  
**Key idea:** Forward noising process + learned reverse denoising  
**Impact:** ⭐⭐⭐⭐⭐

---

## 🚀 Emerging Trends (2024–2025)

### State Space Models

#### [Mamba: Linear-Time Sequence Modeling with Selective State Spaces (2023)](https://arxiv.org/abs/2312.00752)
**Authors:** Gu & Dao  
**Summary:** New architecture that processes sequences in linear time (vs quadratic for Transformers). Matches Transformers on language tasks while being faster on long sequences.  
**Key idea:** Selective state space models with hardware-aware parallelism  
**Why it matters:** Could challenge the Transformer dominance for long-context tasks  
**Impact:** ⭐⭐⭐⭐

---

### Mixture of Experts

#### [Mixtral 8x7B (2024)](https://arxiv.org/abs/2401.04088)
**Authors:** Jiang et al. (Mistral AI)  
**Summary:** Sparse Mixture of Experts model that routes each token to 2 of 8 expert networks. Matches LLaMA-2 70B performance while using only 13B active parameters per token.  
**Key idea:** Sparse routing — not all parameters active at inference  
**Why it matters:** Better compute efficiency for large models  
**Impact:** ⭐⭐⭐⭐

---

### Reasoning

#### [DeepSeek-R1: Reinforcement Learning for Reasoning (2025)](https://arxiv.org/abs/2501.12948)
**Authors:** DeepSeek AI  
**Summary:** Applied reinforcement learning (GRPO) to teach LLMs to reason step-by-step without human-annotated chain-of-thought. Matches OpenAI o1 at a fraction of the cost.  
**Key idea:** RL from outcome rewards (correctness) rather than human demos  
**Why it matters:** Open-source, strong reasoning, cost-efficient  
**Impact:** ⭐⭐⭐⭐⭐

---

### Multimodal & Video

#### [Sora (2024)](https://openai.com/sora)
**Authors:** OpenAI  
**Summary:** Text-to-video model that generates 1-minute+ realistic videos. Treats video as compressed "spacetime patches" fed to a Diffusion Transformer (DiT).  
**Key idea:** Spacetime patch tokenization + Diffusion Transformer  
**Why it matters:** First model to demonstrate world-model-like video understanding  
**Impact:** ⭐⭐⭐⭐⭐

---

### Efficient LLMs

#### [CLaRa: Continuous Latent Representations (2025)](https://machinelearning.apple.com/research/continuous-latent)
**Authors:** Apple  
**Summary:** Encodes multiple tokens into continuous latent representations, enabling end-to-end optimization of the full pipeline. More efficient than discrete tokenization.  
**Key idea:** Unified continuous token representation for compression + generation  
**Why it matters:** Foundation for efficient on-device LLMs  
**Impact:** ⭐⭐⭐⭐

---

## 📥 How to Read a Paper Efficiently

1. **Abstract + Conclusion first** — understand the claim and result
2. **Figures & Tables** — often contains the main contribution visually
3. **Introduction** — motivation and context
4. **Methods** — the technical contribution
5. **Experiments** — what was tested and why
6. **Related work** — what it builds on

> 💡 *Tip: Use [Semantic Scholar](https://www.semanticscholar.org/) or [Papers With Code](https://paperswithcode.com/) to find implementations alongside papers.*
