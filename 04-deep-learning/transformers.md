<![CDATA[# Transformers — The Architecture That Changed Everything

> **Interview weight:** ⭐⭐⭐⭐ — Conceptual understanding is expected at every level.  
> **Time to study:** 5–6 hours.

---

## The Core Innovation: Self-Attention

Instead of processing sequences one step at a time (RNN), transformers compute attention scores between ALL positions simultaneously.

### Scaled Dot-Product Attention

```
Attention(Q, K, V) = softmax(QKᵀ / √d_k) · V
```

- **Q (Query):** "What am I looking for?"
- **K (Key):** "What do I contain?"
- **V (Value):** "What information do I provide?"
- **√d_k:** Scaling factor to prevent softmax from becoming too peaked

```python
import torch
import torch.nn.functional as F

def scaled_dot_product_attention(Q, K, V):
    d_k = Q.size(-1)
    scores = torch.matmul(Q, K.transpose(-2, -1)) / (d_k ** 0.5)
    attention_weights = F.softmax(scores, dim=-1)
    output = torch.matmul(attention_weights, V)
    return output, attention_weights
```

### Multi-Head Attention

Run attention multiple times in parallel with different learned projections.

Each "head" attends to different types of relationships (syntactic, semantic, positional).

```python
import torch.nn as nn

class MultiHeadAttention(nn.Module):
    def __init__(self, d_model, num_heads):
        super().__init__()
        self.num_heads = num_heads
        self.d_k = d_model // num_heads
        
        self.W_q = nn.Linear(d_model, d_model)
        self.W_k = nn.Linear(d_model, d_model)
        self.W_v = nn.Linear(d_model, d_model)
        self.W_o = nn.Linear(d_model, d_model)
    
    def forward(self, Q, K, V):
        batch_size = Q.size(0)
        
        # Linear projections and reshape for multi-head
        Q = self.W_q(Q).view(batch_size, -1, self.num_heads, self.d_k).transpose(1, 2)
        K = self.W_k(K).view(batch_size, -1, self.num_heads, self.d_k).transpose(1, 2)
        V = self.W_v(V).view(batch_size, -1, self.num_heads, self.d_k).transpose(1, 2)
        
        # Scaled dot-product attention
        attn_output, _ = scaled_dot_product_attention(Q, K, V)
        
        # Concatenate heads and project
        attn_output = attn_output.transpose(1, 2).contiguous().view(batch_size, -1, self.num_heads * self.d_k)
        return self.W_o(attn_output)
```

---

## The Transformer Architecture

```
┌──────────────────────────────────────┐
│          ENCODER (×N)                │
│  ┌─────────────────────────┐         │
│  │ Multi-Head Self-Attention│         │
│  │ + Add & LayerNorm       │         │
│  ├─────────────────────────┤         │
│  │ Feed-Forward Network    │         │
│  │ + Add & LayerNorm       │         │
│  └─────────────────────────┘         │
├──────────────────────────────────────┤
│          DECODER (×N)                │
│  ┌─────────────────────────┐         │
│  │ Masked Self-Attention   │         │
│  │ + Add & LayerNorm       │         │
│  ├─────────────────────────┤         │
│  │ Cross-Attention         │         │
│  │ (attend to encoder)     │         │
│  │ + Add & LayerNorm       │         │
│  ├─────────────────────────┤         │
│  │ Feed-Forward Network    │         │
│  │ + Add & LayerNorm       │         │
│  └─────────────────────────┘         │
└──────────────────────────────────────┘
```

### Key Components

| Component | Purpose |
|---|---|
| **Positional Encoding** | Injects position information (since attention has no notion of order) |
| **Layer Normalization** | Stabilizes training |
| **Residual Connections** | Helps gradient flow (same as ResNet) |
| **Feed-Forward Network** | Two linear layers with ReLU: processes each position independently |

---

## Landmark Models

| Model | Architecture | Training Objective | Use Case |
|---|---|---|---|
| **BERT** | Encoder only | Masked language model + next sentence prediction | Classification, NER, QA |
| **GPT** | Decoder only | Next-token prediction (autoregressive) | Text generation, chatbots |
| **T5** | Encoder-decoder | Text-to-text (all tasks framed as text generation) | Translation, summarization |

### Using Pretrained Transformers (HuggingFace)

```python
from transformers import AutoTokenizer, AutoModelForSequenceClassification
import torch

model_name = "distilbert-base-uncased"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForSequenceClassification.from_pretrained(model_name, num_labels=2)

# Tokenize input
inputs = tokenizer("This movie is great!", return_tensors="pt", padding=True, truncation=True)

# Inference
with torch.no_grad():
    outputs = model(**inputs)
    prediction = torch.argmax(outputs.logits, dim=1)
```

---

## Common Interview Questions

1. **Q: Explain self-attention in simple terms.**
   > Each word in a sentence "looks at" every other word and decides how much to pay attention to it. The result is a new representation of each word that incorporates relevant context from the entire sequence.

2. **Q: Why divide by √d_k in attention?**
   > Without scaling, dot products grow with dimension size, pushing softmax into regions with tiny gradients (saturated). Dividing by √d_k keeps the variance of dot products constant regardless of dimension.

3. **Q: What's the difference between BERT and GPT?**
   > BERT uses the encoder (bidirectional — sees full context) and is pretrained with masked language modeling. Best for understanding tasks. GPT uses the decoder (unidirectional — left-to-right) with next-token prediction. Best for generation tasks.

4. **Q: What is the computational complexity of self-attention?**
   > O(n² · d) where n = sequence length, d = model dimension. This quadratic scaling with sequence length is the main bottleneck for long documents.

---

## Resources

- 📖 [The Illustrated Transformer — Jay Alammar](https://jalammar.github.io/illustrated-transformer/)
- 📖 [The Illustrated BERT](https://jalammar.github.io/illustrated-bert/)
- 📺 [Andrej Karpathy — Let's build GPT](https://www.youtube.com/watch?v=kCc8FmEb1nY)
- 📖 [HuggingFace Transformers Docs](https://huggingface.co/docs/transformers/)
]]>
