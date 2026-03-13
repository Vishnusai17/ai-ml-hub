# 🌊 Day 6 — Diffusion Models: Stable Diffusion & DALL-E

**Date:** 2026-03-13  
**Topic:** Diffusion Models — The Science Behind Image Generation  
**Paper:** [Ho et al., 2020 — DDPM](https://arxiv.org/abs/2006.11239)  
**Level:** 🟡 Intermediate

---

## The Core Idea: Destroy, Then Rebuild

Diffusion models learn to **undo noise**. Here's the intuition:

1. **Forward process:** Gradually add Gaussian noise to an image over T steps until it becomes pure noise
2. **Reverse process:** Train a neural network to predict and remove noise step by step — going from pure noise back to a clean image

If the network learns to reverse noise well enough, you can start from random noise and generate a realistic image from scratch.

---

## Forward Process (Adding Noise)

```
Real image x₀ → x₁ → x₂ → ... → xₜ (pure Gaussian noise)
```

Each step adds a small amount of Gaussian noise:
```
xₜ = √(1-β) · xₜ₋₁ + √β · ε     where ε ~ N(0, I)
```

`β` is a small variance schedule — how much noise to add each step.

---

## Reverse Process (Removing Noise)

Train a neural network (usually a U-Net) to predict the noise at each step:
```
Pure noise xₜ → [Denoise] → xₜ₋₁ → [Denoise] → ... → x₀ (clean image)
```

The network learns:
```
εθ(xₜ, t) ≈ ε   (predict the noise that was added at step t)
```

Training loss:
```
L = ||ε - εθ(xₜ, t)||²
```

---

## Latent Diffusion Models (Stable Diffusion)

Running diffusion in pixel space is expensive. **Stable Diffusion** runs diffusion in a **compressed latent space** instead:

```
Image (512×512×3)
    ↓ [Encoder (VAE)]
Latent (64×64×4)   ← diffusion happens here
    ↓ [Decoder (VAE)]
Image (512×512×3)
```

This is ~48x fewer values to process → much faster.

**Text conditioning:** A text prompt is encoded with CLIP and injected into the denoising network via cross-attention at every step.

```
"a cat on mars" → [CLIP text encoder] → text embeddings
                                              ↓
Noisy latent → [U-Net with cross-attention] → less noisy latent
```

---

## Key Components

| Component | Role |
|---|---|
| **VAE Encoder** | Compress image to latent space |
| **VAE Decoder** | Reconstruct image from latent |
| **U-Net** | Denoising network (predicts noise) |
| **CLIP** | Encodes text prompts into embeddings |
| **Noise scheduler** | Controls how noise is added/removed |

---

## Famous Models

| Model | Organization | Notes |
|---|---|---|
| **DDPM** | Ho et al. | Original diffusion paper |
| **DALL-E 2** | OpenAI | CLIP + diffusion, text-to-image |
| **Stable Diffusion** | Stability AI | Open-source, latent diffusion |
| **Midjourney** | Midjourney | Closed, highly aesthetic |
| **Imagen** | Google | T5 text encoder + diffusion |
| **Sora** | OpenAI | Video diffusion (spacetime patches) |

---

## Diffusion vs GANs

| Property | GANs | Diffusion |
|---|---|---|
| Training stability | ❌ Hard, mode collapse | ✅ Stable |
| Sample diversity | Limited | ✅ High |
| Sample quality | Very high | ✅ Very high |
| Inference speed | ✅ Fast (one pass) | ❌ Slow (many steps) |
| Controllability | Moderate | ✅ High (CFG) |

**Classifier-Free Guidance (CFG):** A technique that makes diffusion models follow the text prompt more strongly by steering generation away from unconditional outputs.

---

## 🔗 Resources
- [DDPM Paper](https://arxiv.org/abs/2006.11239)
- [Lilian Weng: What are Diffusion Models?](https://lilianweng.github.io/posts/2021-07-11-diffusion-models/)
- [Illustrated Stable Diffusion](https://jalammar.github.io/illustrated-stable-diffusion/)

---

*Next up → Day 7: Large Language Models — GPT, LLaMA and the Rise of GenAI*
