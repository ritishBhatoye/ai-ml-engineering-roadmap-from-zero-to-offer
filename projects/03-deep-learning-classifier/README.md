<![CDATA[# Project 3: Deep Learning Image Classifier

## 🎯 Objective
Train a CNN in PyTorch for image classification. Demonstrate understanding of deep learning training, tuning, and evaluation.

## 📊 Suggested Datasets
- [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html) — 60K images, 10 classes
- [Fashion-MNIST](https://github.com/zalandoresearch/fashion-mnist) — simpler alternative
- [Chest X-Ray Pneumonia](https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia) — medical imaging

## 📋 Deliverables Checklist

- [ ] **Data loading** — PyTorch DataLoader with augmentation (RandomCrop, HorizontalFlip)
- [ ] **Custom CNN** — build a 3-5 layer CNN from scratch
- [ ] **Training loop** — forward pass, loss, backward pass, optimizer step
- [ ] **Training curves** — plot train/val loss and accuracy per epoch
- [ ] **Transfer learning** — fine-tune a pretrained ResNet/EfficientNet, compare with custom CNN
- [ ] **Evaluation** — confusion matrix, per-class accuracy, sample predictions
- [ ] **Experiment tracking** — log hyperparameters and metrics
- [ ] **README** — architecture diagram, results comparison, how to run

## 🏗 Suggested Structure

```
03-deep-learning-classifier/
├── src/
│   ├── dataset.py
│   ├── model.py
│   ├── train.py
│   └── evaluate.py
├── configs/
│   └── config.yaml
├── results/
│   ├── training_curves.png
│   └── confusion_matrix.png
├── requirements.txt
└── README.md
```

## ⏱ Estimated Time: 15–20 hours
]]>
