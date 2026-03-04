# Project 3: Deep Learning Image Classifier

## Objective

Train a CNN in PyTorch for image classification. Demonstrate understanding of deep learning training, tuning, and evaluation.

**Why this matters:** Shows you can train neural networks, tune hyperparameters, analyze results, and use modern DL tools.

---

## Suggested Datasets

| Dataset | Classes | Images | Difficulty |
|---------|---------|--------|------------|
| CIFAR-10 | 10 | 60K | Beginner-friendly |
| Fashion-MNIST | 10 | 60K | Very simple |
| Chest X-Ray Pneumonia | 2 | 5.8K | Medical imaging |
| Flowers-102 | 102 | 6K | Fine-grained classification |

---

## Deliverables Checklist

### Data Pipeline
- [ ] PyTorch DataLoader with augmentation (RandomCrop, HorizontalFlip, Normalize)
- [ ] Proper train/val/test split
- [ ] Data inspection and sample visualization

### Model
- [ ] Build a custom CNN (3-5 layer) from scratch
- [ ] Implement training loop: forward pass, loss, backward pass, optimizer step
- [ ] Use batch normalization and dropout appropriately

### Training
- [ ] Training curves: plot train/val loss and accuracy per epoch
- [ ] Transfer learning: fine-tune pretrained ResNet/EfficientNet
- [ ] Compare custom CNN vs transfer learning results

### Evaluation
- [ ] Confusion matrix visualization
- [ ] Per-class accuracy analysis
- [ ] Sample predictions with visualizations

### Best Practices
- [ ] Experiment tracking (tensorboard, wandb, or CSV logs)
- [ ] Model checkpointing (save best model)
- [ ] Reproducibility (random seeds)

### Communication
- [ ] README with architecture diagram
- [ ] Results comparison table
- [ ] Key learnings and next steps

---

## Assessment Criteria

| Criterion | Weight | What Interviewers Look For |
|-----------|--------|---------------------------|
| Data Pipeline | 15% | Proper augmentation, correct data loading |
| Model Architecture | 20% | Clean implementation, proper layer sizing |
| Training | 20% | Correct backprop, learning rate scheduling |
| Results Analysis | 20% | Comprehensive evaluation, error analysis |
| Transfer Learning | 15% | Proper fine-tuning strategy |
| Code Quality | 10% | Modular, reproducible, documented |

---

## Suggested Structure

```
03-deep-learning-classifier/
├── src/
│   ├── __init__.py
│   ├── dataset.py              # Data loading & augmentation
│   ├── model.py                # CNN architectures
│   ├── train.py                # Training loop
│   ├── evaluate.py             # Evaluation
│   └── utils.py                # Helpers
├── configs/
│   └── config.yaml             # Hyperparameters
├── notebooks/
│   └── exploration.ipynb       # Experiments
├── results/
│   ├── training_curves.png
│   ├── confusion_matrix.png
│   └── best_model.pt
├── tests/
│   └── test_model.py
├── requirements.txt
└── README.md
```

---

## Starter Code

```python
# src/model.py
import torch
import torch.nn as nn
import torch.optim as optim

class CNN(nn.Module):
    def __init__(self, num_classes=10):
        super(CNN, self).__init__()
        self.features = nn.Sequential(
            # Block 1
            nn.Conv2d(3, 32, kernel_size=3, padding=1),
            nn.BatchNorm2d(32),
            nn.ReLU(),
            nn.MaxPool2d(2),  # 32x32 -> 16x16
            
            # Block 2
            nn.Conv2d(32, 64, kernel_size=3, padding=1),
            nn.BatchNorm2d(64),
            nn.ReLU(),
            nn.MaxPool2d(2),  # 16x16 -> 8x8
            
            # Block 3
            nn.Conv2d(64, 128, kernel_size=3, padding=1),
            nn.BatchNorm2d(128),
            nn.ReLU(),
            nn.MaxPool2d(2),  # 8x8 -> 4x4
        )
        
        self.classifier = nn.Sequential(
            nn.Flatten(),
            nn.Dropout(0.5),
            nn.Linear(128 * 4 * 4, 256),
            nn.ReLU(),
            nn.Dropout(0.3),
            nn.Linear(256, num_classes)
        )
    
    def forward(self, x):
        x = self.features(x)
        x = self.classifier(x)
        return x
```

```python
# src/train.py
import torch
import torch.nn as nn
import torch.optim as optim
from torch.utils.data import DataLoader
from src.model import CNN

def train_one_epoch(model, dataloader, criterion, optimizer, device):
    model.train()
    running_loss = 0.0
    correct = 0
    total = 0
    
    for inputs, labels in dataloader:
        inputs, labels = inputs.to(device), labels.to(device)
        
        optimizer.zero_grad()
        outputs = model(inputs)
        loss = criterion(outputs, labels)
        loss.backward()
        optimizer.step()
        
        running_loss += loss.item()
        _, predicted = outputs.max(1)
        total += labels.size(0)
        correct += predicted.eq(labels).sum().item()
    
    return running_loss / len(dataloader), 100. * correct / total

def train(config):
    device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
    model = CNN(num_classes=10).to(device)
    
    criterion = nn.CrossEntropyLoss()
    optimizer = optim.Adam(model.parameters(), lr=config['lr'])
    scheduler = optim.lr_scheduler.StepLR(optimizer, step_size=10, gamma=0.5)
    
    # Training loop
    for epoch in range(config['epochs']):
        train_loss, train_acc = train_one_epoch(
            model, train_loader, criterion, optimizer, device
        )
        scheduler.step()
        print(f"Epoch {epoch+1}: Loss={train_loss:.4f}, Acc={train_acc:.2f}%")
```

---

## Common Interview Questions for This Project

1. Why did you choose this architecture?
2. Explain the role of batch normalization
3. How did you prevent overfitting?
4. Compare custom CNN vs transfer learning results
5. What would you try next to improve performance?
6. How would you deploy this model for inference?

---

## Transfer Learning Example

```python
import torchvision.models as models

# Load pretrained model
model = models.resnet18(pretrained=True)

# Freeze early layers
for param in model.parameters():
    param.requires_grad = False

# Replace classifier
model.fc = nn.Linear(model.fc.in_features, num_classes)

# Fine-tune last layer
optimizer = optim.Adam(model.fc.parameters(), lr=0.001)
```

---

## Estimated Time: 15–20 hours
