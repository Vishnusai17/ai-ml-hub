# 🎭 Day 5 — Generative Adversarial Networks (GANs)

**Date:** 2026-03-12  
**Topic:** GANs — The Generator vs Discriminator  
**Paper:** [Goodfellow et al., 2014](https://arxiv.org/abs/1406.2661)  
**Level:** 🟡 Intermediate

---

## The Big Idea: A Forger and a Detective

Ian Goodfellow came up with GANs in 2014 at a bar. The idea is elegantly simple:

Train **two networks** against each other:
- **Generator (G)** — creates fake data (images, audio, text). Its job: fool the discriminator.
- **Discriminator (D)** — classifies data as real or fake. Its job: catch the generator.

As they compete, the **generator gets better at faking**, and the **discriminator gets better at detecting**. Eventually the generator produces data indistinguishable from real data.

---

## How Training Works

```
Real images ──→ [Discriminator] ──→ "Real" or "Fake"?
                       ↑
Random noise → [Generator] → Fake image ──→ [Discriminator]
```

**Loss functions:**
- D wants to output 1 for real, 0 for fake
- G wants D to output 1 for its fake images

```python
# Discriminator loss: be correct on both real and fake
L_D = -[log D(real) + log(1 - D(G(z)))]

# Generator loss: fool the discriminator
L_G = -log D(G(z))
```

They're trained in alternating steps — update D, then G, then D, then G...

---

## GAN Architecture

```
z (random noise, e.g. 100-dim vector)
    ↓
[Generator — typically transposed convolutions]
    ↓
Fake image (e.g. 64×64×3)
    ↓
[Discriminator — typically convolutions]
    ↓
Probability: real or fake?
```

---

## Common Problems

| Problem | What Happens | Fix |
|---|---|---|
| **Mode collapse** | Generator produces same output for all inputs | Minibatch discrimination, Wasserstein GAN |
| **Training instability** | Loss oscillates wildly | Learning rate tuning, spectral normalization |
| **Vanishing gradients** | D gets too good too fast, G can't learn | Label smoothing, Wasserstein loss |

---

## Famous GAN Variants

| Model | Year | Achievement |
|---|---|---|
| **DCGAN** | 2015 | First stable image GAN (convolutional) |
| **Pix2Pix** | 2017 | Image-to-image translation (sketch → photo) |
| **CycleGAN** | 2017 | Unpaired image translation (horse → zebra) |
| **StyleGAN** | 2019 | Ultra-realistic face generation |
| **StyleGAN2/3** | 2020/21 | Fixed artifacts, even better quality |
| **BigGAN** | 2018 | High-resolution class-conditional images |

---

## Applications

- 🎨 **Art generation** — creating photorealistic or artistic images
- 👤 **Face synthesis** — "This person does not exist" (thispersondoesnotexist.com)
- 🎬 **Deepfakes** — video face swapping
- 🧬 **Drug discovery** — generating molecular structures
- 📊 **Data augmentation** — generating synthetic training data
- 🖼️ **Image-to-image** — colorization, super-resolution, style transfer

---

## GANs vs Diffusion Models

GANs dominated generative AI from 2014–2021. Then **diffusion models** (Stable Diffusion, DALL-E 2) largely replaced them for image generation because:
- More stable training
- Better mode coverage (don't collapse)
- More controllable

But GANs are still used for **real-time generation** (faster inference than diffusion).

---

## Key Terms

| Term | Meaning |
|---|---|
| **Latent space** | The compressed representation of data (G's input) |
| **Mode collapse** | Generator gets stuck producing one type of output |
| **Wasserstein GAN** | Uses Earth Mover Distance for more stable training |
| **Conditional GAN** | Generator conditioned on a class label or image |

---

## 🔗 Resources
- [Original GAN Paper](https://arxiv.org/abs/1406.2661)
- [GAN Lab — Interactive Visualization](https://poloclub.github.io/ganlab/)
- [thispersondoesnotexist.com](https://thispersondoesnotexist.com) — StyleGAN in action

---

*Next up → Day 6: Diffusion Models — Stable Diffusion & DALL-E*
