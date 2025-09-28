---
title: "Limit Order Book Midpoint prediction for Cryptocurrency Stocks"
excerpt: "Evaluated classical ML model performance and designed light-weight neural networks with custom loss functions for SoTA limit order book midpoint prediction for a cryptocurrency stock"
collection: portfolio
---
## Overview  

From October 2024 to December 2024, I built a system to predict the midpoint price movement in a limit order book (LOB) setting using classical and deep learning methods. The project processes high-frequency bid/ask levels, engineers domain features (like Order Flow Imbalance), and benchmarks multiple models—from KNN to CNN+LSTM to a custom neural-SVR—achieving state-of-the-art performance (MSE ≈ 28.05, R² ≈ 0.998).

---

## Data & Feature Engineering  

- **Conversion of percentages to prices**: Transformed bid/ask distance percentages into absolute price differentials.  
- **Order Flow Imbalance (OFI)**: Computed at 5-depth and 10-depth levels, capturing the net pressure in book dynamics.  
- **Windowing**: Stacked normalized windows of length 100 across time for each sample, to provide temporal context.  

---

## Model Benchmarking & Custom Method  

- **Baseline models tested**:  
  - KNN  
  - SVR  
  - MLP  
  - LSTM  
  - CNN + LSTM  
  - CNN + SVR  
- **Custom method: neural-SVR**  
  - Incorporated a **dynamically scaled ε-insensitive loss**  
  - Added **trend-alignment penalty** to bias predictions to follow directional trends  
- **Evaluation metrics**: Mean Squared Error (MSE) and coefficient of determination (R²)  

**Result highlights**:  

- Achieved **MSE ≈ 28.05**, **R² ≈ 0.998** on held-out test sets  
- Neural-SVR improved trend interpretability by aligning the model’s gradients with price movement direction  

---

## Code & Report Links  

- **Repository code & notebooks**: [GitHub – Limit_Order_Book_Mid_Point_Prediction](https://github.com/prasadboi/Limit_Order_Book_Mid_Point_Prediction)  
- **Project report / write-up**: (available in the same repo; see `report` or `docs` folder)  

---

## Key Contributions  

- Designed domain-specific features (OFI, windowing) that reflect book microstructure rather than plain price series.  
- Evaluated a wide model spectrum, increasing confidence in performance gains.  
- Created a novel **neural-SVR** model tailored to financial prediction challenges (nonlinear, high noise, trend-centric).  
- Demonstrated extremely high R², showing the model captures subtle mid-price dynamics with high fidelity.

---

## Lessons & Next Steps  

- **Takeaways**:  
  - Feature engineering (e.g. OFI) is crucial in HFT-style problems  
  - Regularization and loss design (ε-insensitive, trend penalties) can dramatically aid interpretability  
  - Hybrid models (neural + classical) may outperform purely black-box alternatives  

- **Potential improvements**:  
  - Introduce more book-depth features (e.g. imbalance across 20 levels)  
  - Test on cross-asset and cross-market LOBs  
  - Incorporate attention-based models (Transformers)  
  - Multi-horizon forecasting (predict not only next midpoint, but ahead 5/10 ticks)  

---

### Sample Run (config + script snippet)

1. config.yaml

```yaml
window_size: 100
depth_levels: [5, 10]
models:
  - name: neural_svr
    hidden_dims: [128, 64]
    learning_rate: 1e-4
    eps_init: 0.1
    trend_penalty_weight: 0.01
  - name: cnn_lstm
    filters: [32, 64]
    lstm_hidden: 64
    learning_rate: 1e-3
train:
  batch_size: 32
  epochs: 200
  validation_split: 0.2
```

2. train.py (snippet)

```python
from model import NeuralSVR, build_cnn_lstm
from data import load_lob_windows
import torch
from torch import nn, optim

train_X, train_y, val_X, val_y = load_lob_windows(...)

model = NeuralSVR(hidden_dims=[128,64], eps_init=0.1, trend_penalty=0.01)
criterion = model.custom_loss  # includes eps-insensitive + trend alignment
optimizer = optim.Adam(model.parameters(), lr=1e-4)

for epoch in range(epochs):
    model.train()
    out = model(train_X)
    loss = criterion(out, train_y)
    loss.backward()
    optimizer.step()
    optimizer.zero_grad()

    # Validation & checkpointing
    model.eval()
    with torch.no_grad():
        val_out = model(val_X)
        val_loss = criterion(val_out, val_y)
        # compute MSE, R2 metrics...
```
