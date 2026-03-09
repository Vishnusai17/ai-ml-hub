# 🔍 Day 2 — Convolutional Neural Networks (CNNs)

**Date:** 2026-03-09  
**Topic:** CNNs — Seeing Like a Machine  
**Level:** 🟢 Beginner → 🟡 Intermediate

---

## The Problem with Regular Neural Networks for Images

A 256×256 RGB image has **196,608 input values**. If we feed this into a standard (fully connected) neural network, the first hidden layer alone could need hundreds of millions of weights. This is:
- Computationally expensive
- Prone to overfitting
- Doesn't respect spatial structure (a pixel's neighbors matter!)

CNNs solve all three problems.

---

## The Core Idea: Filters

Instead of connecting every pixel to every neuron, a CNN slides a small **filter (kernel)** across the image. A 3×3 filter looks at 9 pixels at a time, learning to detect a specific pattern — an edge, a curve, a texture.

```
Image patch:        Filter:          Output (dot product):
[1, 0, 1]          [1, 0, -1]
[0, 1, 0]    ·     [1, 0, -1]   →   single number
[1, 0, 1]          [1, 0, -1]
```

Slide this filter across the entire image → you get a **feature map** showing where that pattern appears.

---

## CNN Architecture

A CNN stacks these building blocks:

### 1. Convolutional Layer
- Applies multiple filters to the input
- Each filter detects a different feature (edge, color gradient, texture)
- Output: a set of feature maps

### 2. Activation (ReLU)
- Adds non-linearity after each conv layer
- `output = max(0, x)` — keeps positive values, zeros out negatives

### 3. Pooling Layer
- **Max pooling** — takes the max value in each small region
- Reduces spatial size → fewer parameters, more robust
- A face detector shouldn't care if the face is 2px to the left

### 4. Fully Connected Layer
- At the end, flatten the feature maps
- Connect to output neurons for classification

```
Input Image
    ↓
[Conv → ReLU] × N     ← learn local features
    ↓
[Pooling]             ← reduce size
    ↓
[Flatten]
    ↓
[Fully Connected]     ← classify
    ↓
Output (class scores)
```

---

## What CNNs Learn Layer by Layer

| Layer Depth | What's Detected |
|---|---|
| Early layers | Edges, lines, colors |
| Middle layers | Shapes, textures, patterns |
| Deep layers | Parts of objects (eyes, wheels) |
| Final layers | Full objects (cat, car) |

This is why **transfer learning** works: early layers learn universal features. A model trained on ImageNet already knows edges and textures — you just fine-tune the later layers.

---

## Famous CNN Architectures

| Model | Year | Key Innovation |
|---|---|---|
| **LeNet-5** | 1998 | First practical CNN (digit recognition) |
| **AlexNet** | 2012 | Deep CNN + GPU training, won ImageNet |
| **VGG-16** | 2014 | Very deep (16 layers), simple 3×3 filters |
| **ResNet** | 2015 | Skip connections → train 150+ layer networks |
| **EfficientNet** | 2019 | Optimal depth/width/resolution scaling |
| **ViT** | 2021 | Transformer applied to image patches |

---

## Key Terms

| Term | Meaning |
|---|---|
| **Filter/Kernel** | Small learnable matrix that slides over input |
| **Feature Map** | Output of applying a filter to an input |
| **Stride** | How many pixels the filter moves each step |
| **Padding** | Adding zeros around the border to preserve size |
| **Pooling** | Down-sampling to reduce spatial dimensions |
| **Receptive Field** | Region of input a neuron can "see" |

---

## 🔗 Resources
- [CS231n: CNNs for Visual Recognition](http://cs231n.stanford.edu/)
- [3Blue1Brown + Grant + Convo: How CNNs work visually](https://www.youtube.com/watch?v=KuXjwB4LzSA)
- [Papers With Code: Image Classification](https://paperswithcode.com/task/image-classification)

---

*Next up → Day 3: RNNs & LSTMs — Memory for Sequences*
