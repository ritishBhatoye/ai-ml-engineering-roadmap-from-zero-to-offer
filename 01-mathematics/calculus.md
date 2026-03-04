<![CDATA[# Calculus for Machine Learning

> **Interview weight:** ⭐⭐ — Rarely tested directly, but essential for understanding gradient descent.  
> **Time to study:** 3–4 hours.  
> **Goal:** Understand derivatives, gradients, and the chain rule as they apply to optimization in ML.

---

## What Interviewers Actually Test

They won't ask you to solve integrals. They **will** ask:

- "How does gradient descent work?"
- "What is the learning rate and what happens if it's too high or too low?"
- "Explain backpropagation"
- "Why does the chain rule matter in neural networks?"

---

## Core Concepts

### 1. Derivatives — The Slope of a Function

The derivative f'(x) tells you how fast f(x) changes as x changes.

```
f(x) = x²       →  f'(x) = 2x
f(x) = x³       →  f'(x) = 3x²
f(x) = eˣ       →  f'(x) = eˣ
f(x) = ln(x)    →  f'(x) = 1/x
f(x) = 1/(1+e⁻ˣ) → f'(x) = f(x)·(1 - f(x))   ← sigmoid derivative!
```

**ML relevance:** When we minimize a loss function, we need its derivative to know which direction to move the weights.

### 2. Partial Derivatives

When a function has multiple variables, partial derivatives tell you how the function changes with respect to each variable **independently.**

```
f(x, y) = x² + 3xy + y²

∂f/∂x = 2x + 3y      (treat y as constant)
∂f/∂y = 3x + 2y      (treat x as constant)
```

### 3. The Gradient

The gradient is the vector of all partial derivatives. It points in the direction of steepest ascent.

```
∇f(x, y) = [∂f/∂x, ∂f/∂y] = [2x + 3y, 3x + 2y]
```

**To minimize a function:** Move in the **opposite** direction of the gradient.

### 4. Gradient Descent

The core optimization algorithm in ML:

```
θ_new = θ_old - α · ∇L(θ)
```

Where:
- θ = model parameters (weights)
- α = learning rate
- ∇L(θ) = gradient of the loss function

```python
import numpy as np

# Gradient descent for linear regression: minimize MSE loss
# L(w) = (1/n) Σ (y - Xw)²
# ∇L(w) = -(2/n) Xᵀ(y - Xw)

def gradient_descent(X, y, lr=0.01, epochs=1000):
    n, d = X.shape
    w = np.zeros(d)
    
    for epoch in range(epochs):
        predictions = X @ w
        error = y - predictions
        gradient = -(2 / n) * (X.T @ error)
        w = w - lr * gradient
        
        if epoch % 100 == 0:
            loss = np.mean(error ** 2)
            print(f"Epoch {epoch}: Loss = {loss:.4f}")
    
    return w
```

### 5. Learning Rate Effects

| Learning Rate | Behavior |
|---|---|
| **Too small** (e.g., 0.00001) | Converges very slowly, may get stuck |
| **Good** (e.g., 0.001–0.01) | Smooth convergence to minimum |
| **Too large** (e.g., 1.0) | Oscillates wildly, may diverge |

**Interview insight:** This is why we use learning rate schedulers (e.g., reduce on plateau, cosine annealing) — start fast, slow down near the minimum.

### 6. Chain Rule — The Backbone of Backpropagation

If f = g(h(x)), then:

```
df/dx = dg/dh · dh/dx
```

**Why this matters for neural networks:**

In a 3-layer network: `output = f₃(f₂(f₁(x)))`

To compute how the loss changes with respect to weights in layer 1:

```
∂L/∂w₁ = ∂L/∂f₃ · ∂f₃/∂f₂ · ∂f₂/∂f₁ · ∂f₁/∂w₁
```

This is **backpropagation** — applying the chain rule backwards through the network.

```python
# Simple example: 2-layer network forward + backward pass
# Forward: z1 = x*w1, a1 = relu(z1), z2 = a1*w2, loss = (y - z2)²

def forward_backward(x, y, w1, w2, lr=0.01):
    # Forward pass
    z1 = x * w1
    a1 = max(0, z1)         # ReLU
    z2 = a1 * w2
    loss = (y - z2) ** 2
    
    # Backward pass (chain rule)
    dL_dz2 = -2 * (y - z2)  # ∂L/∂z2
    dL_dw2 = dL_dz2 * a1    # ∂L/∂w2 = ∂L/∂z2 · ∂z2/∂w2
    dL_da1 = dL_dz2 * w2    # ∂L/∂a1 = ∂L/∂z2 · ∂z2/∂a1
    dL_dz1 = dL_da1 * (1 if z1 > 0 else 0)  # ReLU derivative
    dL_dw1 = dL_dz1 * x     # ∂L/∂w1 = ∂L/∂z1 · ∂z1/∂w1
    
    # Update weights
    w1 -= lr * dL_dw1
    w2 -= lr * dL_dw2
    
    return w1, w2, loss
```

### 7. Variants of Gradient Descent

| Variant | Update Rule | Pros | Cons |
|---|---|---|---|
| **Batch GD** | Use ALL data for each update | Stable gradient | Slow on large datasets |
| **Stochastic GD (SGD)** | Use 1 sample per update | Fast, can escape local minima | Noisy updates |
| **Mini-batch GD** | Use a batch (32–256 samples) | Best of both worlds | Most common in practice |
| **Adam** | Adaptive learning rate per parameter | Fast convergence, robust | Can overfit; may generalize worse than SGD |

---

## Common Interview Questions

1. **Q: Explain gradient descent in simple terms.**
   > Imagine you're on a foggy mountain and want to reach the lowest point. You feel the slope under your feet and take a step downhill. Gradient descent does this for the loss function — it computes the slope (gradient) and moves the parameters downhill.

2. **Q: What is vanishing gradient, and why is it a problem?**
   > In deep networks, gradients are multiplied through many layers (chain rule). If each gradient is < 1, the product becomes exponentially small — early layers barely learn. Solutions: ReLU activations, residual connections, LSTMs.

3. **Q: Why do we use Adam instead of vanilla SGD?**
   > Adam maintains per-parameter adaptive learning rates using first and second moment estimates of gradients. It converges faster on most problems. However, SGD with momentum + scheduling often generalizes better.

4. **Q: What's the relationship between the loss function and the gradient?**
   > The gradient of the loss function with respect to model parameters tells us the direction and magnitude to adjust each parameter to reduce the loss. The loss function defines WHAT we optimize; the gradient defines HOW.

---

## Try It Yourself

1. Implement gradient descent for logistic regression from scratch (no sklearn).
2. Visualize convergence: plot loss vs epoch for different learning rates (too small, good, too large).
3. Implement the backward pass for a 2-layer neural network manually (compute all gradients by hand, then verify with PyTorch's `autograd`).

---

## Resources

- 📺 [3Blue1Brown — Essence of Calculus](https://www.youtube.com/playlist?list=PLZHQObOWTQDMsr9K-rj53DwVRMYO3t5Yr)
- 📺 [3Blue1Brown — Neural Networks (backpropagation episode)](https://www.youtube.com/watch?v=Ilg3gGewQ5U)
- 📖 [Mathematics for Machine Learning — Chapter 5](https://mml-book.github.io/)
]]>
