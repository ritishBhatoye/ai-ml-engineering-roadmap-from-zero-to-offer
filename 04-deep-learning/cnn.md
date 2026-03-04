<![CDATA[# Convolutional Neural Networks (CNN)

> **Interview weight:** ⭐⭐⭐⭐ — Tested in DL-focused roles; conceptual understanding expected everywhere.  
> **Time to study:** 6–8 hours.

---

## Core Operations

### Convolution

A filter (kernel) slides across the input, computing element-wise products and summing.

```
Input:  5×5        Filter: 3×3        Output: 3×3
┌─────────────┐    ┌─────────┐        ┌─────────┐
│ 1 0 1 0 1   │    │ 1 0 1   │        │ 4 3 4   │
│ 0 1 0 1 0   │ *  │ 0 1 0   │   =    │ 2 4 3   │
│ 1 0 1 0 1   │    │ 1 0 1   │        │ 4 3 4   │
│ 0 1 0 1 0   │    └─────────┘        └─────────┘
│ 1 0 1 0 1   │
└─────────────┘
```

**Output size:** `(input_size - kernel_size + 2*padding) / stride + 1`

### Pooling

Reduces spatial dimensions. Max pooling keeps the most prominent features.

```python
import torch.nn as nn

# Max pooling with 2×2 window → halves spatial dimensions
nn.MaxPool2d(kernel_size=2, stride=2)

# Average pooling
nn.AvgPool2d(kernel_size=2, stride=2)
```

---

## A Complete CNN in PyTorch

```python
import torch
import torch.nn as nn

class CNN(nn.Module):
    def __init__(self, num_classes=10):
        super().__init__()
        self.features = nn.Sequential(
            # Conv Block 1: 3 → 32 channels
            nn.Conv2d(3, 32, kernel_size=3, padding=1),
            nn.BatchNorm2d(32),
            nn.ReLU(),
            nn.MaxPool2d(2, 2),          # 32×32 → 16×16
            
            # Conv Block 2: 32 → 64 channels
            nn.Conv2d(32, 64, kernel_size=3, padding=1),
            nn.BatchNorm2d(64),
            nn.ReLU(),
            nn.MaxPool2d(2, 2),          # 16×16 → 8×8
            
            # Conv Block 3: 64 → 128 channels
            nn.Conv2d(64, 128, kernel_size=3, padding=1),
            nn.BatchNorm2d(128),
            nn.ReLU(),
            nn.AdaptiveAvgPool2d((1, 1)),  # Global average pooling
        )
        
        self.classifier = nn.Sequential(
            nn.Flatten(),
            nn.Dropout(0.5),
            nn.Linear(128, num_classes),
        )
    
    def forward(self, x):
        x = self.features(x)
        x = self.classifier(x)
        return x
```

---

## Key Architecture Milestones

| Architecture | Year | Key Innovation | Depth |
|---|---|---|---|
| **LeNet-5** | 1998 | Basic CNN for digit recognition | 5 layers |
| **AlexNet** | 2012 | ReLU, dropout, GPU training | 8 layers |
| **VGGNet** | 2014 | Small (3×3) filters, deep stacking | 16–19 layers |
| **ResNet** | 2015 | **Skip connections** — solved vanishing gradients for deep networks | 50–152 layers |
| **EfficientNet** | 2019 | Compound scaling (width × depth × resolution) | Varies |

**Interview Q: What is a skip (residual) connection and why does it work?**
> A skip connection adds the input of a layer directly to its output: `output = F(x) + x`. This allows gradients to flow directly through the addition, preventing vanishing gradients. It also makes it easy for the network to learn the identity function if a layer is unnecessary.

---

## Transfer Learning

**The most practical technique in deep learning.**

Instead of training from scratch, use a model pretrained on ImageNet and fine-tune.

```python
import torchvision.models as models

# Load pretrained ResNet-18
model = models.resnet18(pretrained=True)

# Freeze feature extractor
for param in model.parameters():
    param.requires_grad = False

# Replace the final classification layer
model.fc = nn.Linear(512, num_classes)

# Only train the new layer
optimizer = torch.optim.Adam(model.fc.parameters(), lr=0.001)
```

**When to use transfer learning:**
- Small dataset (< 10K images) → Always use it
- Medium dataset (10K–100K) → Fine-tune the last few layers
- Large dataset (> 100K) → Can train from scratch, but pretrained init still helps

---

## Common Interview Questions

1. **Q: How does a convolutional layer differ from a fully connected layer?**
   > A conv layer uses shared weights (the same filter applied across all spatial positions), which captures local patterns and reduces parameters. A fully connected layer connects every neuron to every neuron in the next layer — much more parameters, no spatial awareness.

2. **Q: Why use convolutions for images instead of fully connected layers?**
   > (1) **Parameter efficiency:** A 3×3 filter has 9 parameters regardless of image size. (2) **Translation invariance:** The same filter detects the same pattern anywhere in the image. (3) **Spatial hierarchy:** Stacking conv layers learns low-level features (edges) → mid-level (textures) → high-level (objects).

3. **Q: What does increasing the number of filters do?**
   > Each filter learns to detect a different feature. More filters → more features detected → more model capacity. But also more parameters and computation.

4. **Q: How do you handle different input image sizes?**
   > Use `AdaptiveAvgPool2d` before the classifier — it outputs a fixed-size feature map regardless of input dimensions. Or resize all inputs to the same size during preprocessing.

---

## Resources

- 📺 [Stanford CS231n — CNNs for Visual Recognition](https://cs231n.stanford.edu/)
- 📖 [Deep Learning Book — Chapter 9](https://www.deeplearningbook.org/)
- 📖 [PyTorch Transfer Learning Tutorial](https://pytorch.org/tutorials/beginner/transfer_learning_tutorial.html)
]]>
