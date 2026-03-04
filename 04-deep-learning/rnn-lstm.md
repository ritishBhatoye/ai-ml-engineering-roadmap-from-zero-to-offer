<![CDATA[# RNNs & LSTMs — Sequence Modeling

> **Interview weight:** ⭐⭐⭐  
> **Time to study:** 5–6 hours.

---

## Recurrent Neural Networks

**Idea:** Process sequences by maintaining a hidden state across time steps.

```
h_t = tanh(W_hh · h_{t-1} + W_xh · x_t + b)
y_t = W_hy · h_t
```

### The Vanishing Gradient Problem

Gradients are multiplied through each time step during backpropagation through time (BPTT). With tanh (gradient ≤ 1), they shrink exponentially → early time steps don't learn.

---

## LSTM (Long Short-Term Memory)

Solves vanishing gradients with a cell state and three gates:

- **Forget gate:** What to discard from cell state
- **Input gate:** What new info to store
- **Output gate:** What to output from cell state

The cell state flows through with minimal transformation (addition), allowing gradients to propagate unchanged.

```python
import torch.nn as nn

class LSTMClassifier(nn.Module):
    def __init__(self, vocab_size, embed_dim, hidden_dim, output_dim):
        super().__init__()
        self.embedding = nn.Embedding(vocab_size, embed_dim)
        self.lstm = nn.LSTM(embed_dim, hidden_dim, num_layers=2,
                            batch_first=True, dropout=0.3, bidirectional=True)
        self.fc = nn.Linear(hidden_dim * 2, output_dim)
        self.dropout = nn.Dropout(0.5)
    
    def forward(self, x):
        embedded = self.dropout(self.embedding(x))
        output, (hidden, cell) = self.lstm(embedded)
        hidden = torch.cat((hidden[-2], hidden[-1]), dim=1)
        return self.fc(self.dropout(hidden))
```

## GRU — Simpler Alternative

2 gates (reset + update) instead of 3. Fewer parameters, similar performance.

## Why Transformers Replaced RNNs

| RNN Issue | Transformer Fix |
|---|---|
| Sequential → can't parallelize | Self-attention processes all positions at once |
| Long-range info decays | Attention directly connects any positions |
| Slow GPU utilization | Matrix multiplications are parallelizable |

## Common Interview Questions

1. **Q: How do LSTMs solve vanishing gradients?**
   > The cell state is updated through addition (not multiplication), providing a gradient highway. Gates control what info is retained or added.

2. **Q: LSTM vs GRU?**
   > GRU: 2 gates, fewer parameters, faster. LSTM: 3 gates, slightly better for very long dependencies.

3. **Q: When would you still use an RNN?**
   > Small datasets, real-time streaming, memory constraints with very long sequences.

## Resources

- 📖 [Understanding LSTMs — Colah's Blog](https://colah.github.io/posts/2015-08-Understanding-LSTMs/)
- 📺 [StatQuest — LSTM](https://www.youtube.com/watch?v=YCzL96nL7j0)
]]>
