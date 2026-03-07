# 🔥 Deep Learning Curriculum

Structured learning path from neural net fundamentals to cutting-edge architectures.

---

## 📍 Phase 1 — Neural Network Fundamentals (Weeks 1–3)

### Core Concepts
| Concept | Resource |
|---|---|
| What is a neural network? | [3Blue1Brown Neural Networks Series](https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi) |
| Backpropagation | [Andrej Karpathy — makemore series](https://www.youtube.com/playlist?list=PLAqhIrjkxbuWI23v9cThsA9GvCAUhRvKZ) |
| Activation functions | ReLU, Sigmoid, Tanh, GELU |
| Loss functions | MSE, Cross-Entropy, Focal Loss |
| Optimizers | SGD, Adam, AdamW, Lion |
| Regularization | Dropout, BatchNorm, LayerNorm, Weight Decay |

**Implement:** XOR problem → MNIST from scratch in NumPy

---

## 📍 Phase 2 — Convolutional Neural Networks (Weeks 4–6)

| Topic | Resource |
|---|---|
| Conv layers, pooling, receptive fields | [CS231n Stanford](http://cs231n.stanford.edu/) |
| Classic architectures | AlexNet → VGG → ResNet → EfficientNet |
| Transfer Learning | Fine-tuning pretrained models (torchvision) |
| Object Detection | YOLO, Faster R-CNN, DETR |
| Image Segmentation | U-Net, Mask R-CNN, SAM |

**Project:** Image classifier → Object detector on custom dataset

---

## 📍 Phase 3 — Sequence Models (Weeks 7–9)

| Topic | Resource |
|---|---|
| RNNs & LSTMs | [Colah's LSTM Blog](https://colah.github.io/posts/2015-08-Understanding-LSTMs/) |
| Seq2Seq & Encoder-Decoder | Machine translation fundamentals |
| Attention Mechanism | [The Illustrated Attention](https://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/) |
| Transformers (from scratch) | [Andrej Karpathy — nanoGPT](https://github.com/karpathy/nanoGPT) |

---

## 📍 Phase 4 — Modern Architectures (Weeks 10–14)

### Large Language Models
| Topic | Resource |
|---|---|
| GPT Architecture | [Illustrated GPT-2](https://jalammar.github.io/illustrated-gpt2/) |
| BERT & Fine-tuning | [HuggingFace Course](https://huggingface.co/learn/nlp-course/) |
| Prompt Engineering | [OpenAI Cookbook](https://cookbook.openai.com/) |
| RLHF & Alignment | [Anthropic Constitutional AI](https://arxiv.org/abs/2212.08073) |
| RAG (Retrieval-Augmented Generation) | [LangChain Docs](https://python.langchain.com/) |

### Vision-Language Models
| Model | Paper | Use Case |
|---|---|---|
| CLIP | [arxiv](https://arxiv.org/abs/2103.00020) | Zero-shot image classification |
| BLIP-2 | [arxiv](https://arxiv.org/abs/2301.12597) | Image captioning, VQA |
| GPT-4V | OpenAI | Multimodal reasoning |
| LLaVA | [arxiv](https://arxiv.org/abs/2304.08485) | Open-source multimodal |

### Generative Models
| Model | Paper | Use Case |
|---|---|---|
| VAE | [Kingma & Welling 2013](https://arxiv.org/abs/1312.6114) | Latent representation |
| GAN | [Goodfellow et al. 2014](https://arxiv.org/abs/1406.2661) | Image synthesis |
| Diffusion Models | [Ho et al. 2020](https://arxiv.org/abs/2006.11239) | Image/video generation |
| Stable Diffusion | [Rombach et al. 2022](https://arxiv.org/abs/2112.10752) | Latent diffusion |

---

## 📍 Phase 5 — Emerging Architectures (2024–2025)

| Architecture | Key Idea | Paper |
|---|---|---|
| Mamba / SSM | Linear-time sequence models | [arxiv](https://arxiv.org/abs/2312.00752) |
| Mixture of Experts | Route tokens to specialized sub-networks | [Mixtral](https://arxiv.org/abs/2401.04088) |
| Vision Mamba | SSM applied to vision | [arxiv](https://arxiv.org/abs/2401.13660) |
| KAN (Kolmogorov-Arnold Networks) | Learnable activation functions | [arxiv](https://arxiv.org/abs/2404.19756) |

---

## 🛠️ Frameworks

| Framework | Best For |
|---|---|
| **PyTorch** | Research, flexibility, most papers |
| **TensorFlow / Keras** | Production, mobile (TFLite) |
| **JAX** | High-performance research, Google TPUs |
| **HuggingFace Transformers** | Pre-trained models, fine-tuning |
| **Lightning** | Cleaner PyTorch training loops |

---

## 📚 Full Courses

| Course | Provider | Free? |
|---|---|---|
| Deep Learning Specialization | Coursera (Andrew Ng) | Audit free |
| CS231n: CNNs | Stanford | ✅ |
| CS224n: NLP with DL | Stanford | ✅ |
| fast.ai Practical DL | fast.ai | ✅ |
| Full Stack Deep Learning | FSDL | ✅ |
| HuggingFace NLP Course | HuggingFace | ✅ |
