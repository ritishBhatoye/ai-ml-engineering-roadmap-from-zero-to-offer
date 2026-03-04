<![CDATA[# Neural Network Basics — Foundations of Deep Learning

> **Interview weight:** ⭐⭐⭐⭐ — Core concepts are tested even for ML-focused (not DL-focused) roles.  
> **Time to study:** 5–6 hours.

---

## The Building Blocks

### A Single Neuron (Perceptron)

```
inputs: x₁, x₂, ..., xₙ
weights: w₁, w₂, ..., wₙ
bias: b

z = w₁x₁ + w₂x₂ + ... + wₙxₙ + b  (linear combination)
a = σ(z)                              (activation function)
```

A neural network is just **layers of neurons** connected together.

### Activation Functions

| Function | Formula | Output Range | When to Use |
|---|---|---|---|
| **ReLU** | max(0, z) | [0, ∞) | Hidden layers (default choice) |
| **Sigmoid** | 1 / (1 + e⁻ᶻ) | (0, 1) | Binary classification output |
| **Softmax** | eᶻⁱ / Σeᶻʲ | (0, 1), sums to 1 | Multi-class output |
| **Tanh** | (eᶻ - e⁻ᶻ) / (eᶻ + e⁻ᶻ) | (-1, 1) | RNNs, sometimes hidden layers |
| **Leaky ReLU** | max(0.01z, z) | (-∞, ∞) | When dying ReLU is a problem |

**Interview Q: Why do we need activation functions?**
> Without activations, a multi-layer network is just a single linear transformation (matrix multiplication is closed under composition). Activations introduce non-linearity, allowing the network to learn complex patterns.

### Loss Functions

| Task | Loss Function | PyTorch |
|---|---|---|
| Binary classification | Binary Cross-Entropy | `nn.BCEWithLogitsLoss()` |
| Multi-class classification | Categorical Cross-Entropy | `nn.CrossEntropyLoss()` |
| Regression | MSE | `nn.MSELoss()` |

---

## Forward Pass & Backpropagation

### Forward Pass

Data flows through the network: input → hidden layers → output → loss.

```python
import torch
import torch.nn as nn

class SimpleNN(nn.Module):
    def __init__(self, input_dim, hidden_dim, output_dim):
        super().__init__()
        self.fc1 = nn.Linear(input_dim, hidden_dim)
        self.relu = nn.ReLU()
        self.fc2 = nn.Linear(hidden_dim, output_dim)
    
    def forward(self, x):
        x = self.fc1(x)
        x = self.relu(x)
        x = self.fc2(x)
        return x

model = SimpleNN(input_dim=10, hidden_dim=64, output_dim=1)
```

### Backpropagation

Gradients flow backward: loss → output → hidden layers → input.

Uses the **chain rule** to compute ∂Loss/∂weight for every weight in the network.

```python
# PyTorch handles backpropagation automatically
criterion = nn.BCEWithLogitsLoss()
optimizer = torch.optim.Adam(model.parameters(), lr=0.001)

# Training loop
for epoch in range(100):
    optimizer.zero_grad()           # Reset gradients
    output = model(X_train_tensor)  # Forward pass
    loss = criterion(output, y_train_tensor)  # Compute loss
    loss.backward()                 # Backward pass (compute gradients)
    optimizer.step()                # Update weights
```

---

## Training a Neural Network — Full Pipeline

```python
import torch
from torch.utils.data import DataLoader, TensorDataset

# 1. Prepare data
X_train_tensor = torch.FloatTensor(X_train)
y_train_tensor = torch.FloatTensor(y_train).unsqueeze(1)
dataset = TensorDataset(X_train_tensor, y_train_tensor)
train_loader = DataLoader(dataset, batch_size=32, shuffle=True)

# 2. Define model
model = SimpleNN(input_dim=10, hidden_dim=64, output_dim=1)

# 3. Loss and optimizer
criterion = nn.BCEWithLogitsLoss()
optimizer = torch.optim.Adam(model.parameters(), lr=0.001, weight_decay=1e-4)

# 4. Training loop
for epoch in range(50):
    model.train()
    total_loss = 0
    for X_batch, y_batch in train_loader:
        optimizer.zero_grad()
        output = model(X_batch)
        loss = criterion(output, y_batch)
        loss.backward()
        optimizer.step()
        total_loss += loss.item()
    
    # Validation
    model.eval()
    with torch.no_grad():
        val_output = model(X_val_tensor)
        val_loss = criterion(val_output, y_val_tensor)
    
    print(f"Epoch {epoch}: Train Loss={total_loss/len(train_loader):.4f}, Val Loss={val_loss:.4f}")
```

---

## Key Concepts

### Batch Size

| Size | Pros | Cons |
|---|---|---|
| Small (16–64) | Better generalization, lower memory | Noisy gradients, slower convergence |
| Large (256–1024) | Faster training, stable gradients | Can overfit, may need warmup |

### Learning Rate

The most important hyperparameter. Use a learning rate finder:

```python
# Start with 1e-3 for Adam, 1e-2 for SGD
# Reduce on plateau:
scheduler = torch.optim.lr_scheduler.ReduceLROnPlateau(
    optimizer, mode='min', factor=0.5, patience=5
)
```

### Common Problems

| Problem | Symptom | Solution |
|---|---|---|
| **Vanishing gradients** | Early layers don't learn | Use ReLU, BatchNorm, skip connections |
| **Exploding gradients** | Loss becomes NaN | Gradient clipping, lower learning rate |
| **Dying ReLU** | Neurons output 0 permanently | Use Leaky ReLU or PReLU |
| **Overfitting** | Train loss ↓, val loss ↑ | Dropout, early stopping, more data |

---

## Common Interview Questions

1. **Q: Explain backpropagation step by step.**
   > (1) Forward pass: compute predictions and loss. (2) Compute the gradient of the loss with respect to the output layer weights (using the chain rule). (3) Propagate gradients backward through each layer. (4) Update all weights using the gradients and learning rate.

2. **Q: What is batch normalization and why does it help?**
   > BatchNorm normalizes the inputs to each layer to have zero mean and unit variance (within each mini-batch). Benefits: (1) Stabilizes training. (2) Allows higher learning rates. (3) Reduces sensitivity to weight initialization. (4) Acts as mild regularization.

3. **Q: How does Adam optimizer work?**
   > Adam maintains two moving averages for each parameter: (1) first moment (mean of gradients = momentum), (2) second moment (mean of squared gradients = adaptive learning rate). It combines SGD with momentum and RMSProp.

---

## Resources

- 📺 [3Blue1Brown — Neural Networks](https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi)
- 📖 [PyTorch Official Tutorials](https://pytorch.org/tutorials/)
- 📖 [Deep Learning Book — Chapter 6](https://www.deeplearningbook.org/)
]]>
