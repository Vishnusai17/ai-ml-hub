# 🧠 Day 1 — What is a Neural Network?

**Date:** 2026-03-08  
**Topic:** Foundations of Deep Learning  
**Level:** 🟢 Beginner

---

## The Big Idea

Every deep learning model — whether it's GPT, Stable Diffusion, or a self-driving car — is built on one foundational concept: **the neural network**.

A neural network is a system loosely inspired by the human brain. It learns patterns from data by adjusting millions (or billions) of small numerical weights through a process called **training**.

---

## How It Works

A neural network has three types of layers:

```
Input Layer  →  Hidden Layers  →  Output Layer
[1, 0, 1]   →  [computations]  →  [0.92]
```

1. **Input Layer** — receives raw data (pixel values, numbers, words)
2. **Hidden Layers** — transform the data through learned weights and activation functions
3. **Output Layer** — produces the final prediction (a class, a number, a token)

Each connection between neurons has a **weight** — a number that controls how much influence one neuron has on the next.

---

## The Neuron

A single neuron does three things:

1. **Weighted sum** — multiply each input by its weight and add them up
2. **Bias** — add a constant offset
3. **Activation function** — apply a non-linear transformation

```python
output = activation(w1*x1 + w2*x2 + w3*x3 + bias)
```

Without the activation function, the entire network would just be a linear function — no matter how many layers you stack. Common activation functions:

| Name | Formula | When Used |
|---|---|---|
| ReLU | max(0, x) | Hidden layers (most common) |
| Sigmoid | 1/(1+e^-x) | Binary output |
| Softmax | e^x / Σe^x | Multi-class output |
| GELU | x·Φ(x) | Transformers |

---

## How Neurons Learn — Backpropagation

Training works in two passes:

**Forward pass:** data flows through the network → produces a prediction

**Loss function:** measures how wrong the prediction is
```python
loss = (prediction - actual)²   # Mean Squared Error
```

**Backward pass (backpropagation):** computes how much each weight contributed to the error using the chain rule of calculus

**Optimizer:** updates the weights to reduce the loss
```python
weight = weight - learning_rate * gradient
```

Repeat millions of times → the network gets better.

---

## Types of Neural Networks

| Type | Best For | Key Feature |
|---|---|---|
| **Feedforward (MLP)** | Tabular data, regression | Fully connected layers |
| **CNN** | Images, video | Convolutional filters |
| **RNN / LSTM** | Text, time series | Memory across time steps |
| **Transformer** | NLP, vision, multimodal | Attention mechanism |
| **GAN** | Image generation | Generator + Discriminator |
| **Diffusion** | Image/video generation | Iterative denoising |
| **GNN** | Graphs, molecules | Propagation over graph edges |

---

## Key Concepts Summary

| Term | Meaning |
|---|---|
| **Weight** | Learnable parameter connecting neurons |
| **Bias** | Offset added to the weighted sum |
| **Activation** | Non-linearity applied to each neuron |
| **Loss** | How wrong the model's prediction is |
| **Backprop** | Computing gradients via chain rule |
| **Optimizer** | Algorithm that updates weights |
| **Epoch** | One full pass through the training data |
| **Batch size** | Samples processed before a weight update |

---

## 🔗 Resources
- [3Blue1Brown: Neural Networks](https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi)
- [Andrej Karpathy: Micrograd](https://github.com/karpathy/micrograd) — build backprop from scratch in ~100 lines
- [Playground.tensorflow.org](https://playground.tensorflow.org) — interactive neural network in your browser

---

*Next up → Day 2: Convolutional Neural Networks (CNNs)*
