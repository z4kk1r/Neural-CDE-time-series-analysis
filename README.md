# Neural Controlled Differential Equations for Robust Time Series Prediction

This repository contains a PyTorch implementation and reproduction of the paper:  
**"Neural Controlled Differential Equations for Irregular Time Series"** (Kidger et al., NeurIPS 2020).

The project focuses on demonstrating the mathematical and engineering advantages of modeling time series as continuous paths using differential equations, specifically comparing **Neural CDEs** against traditional **LSTMs**.

## Key Features
- **Continuous-time Modeling:** Uses Natural Cubic Splines to handle irregular sampling.
- **Robustness Analysis:** Extensive stress tests involving missing data (up to 90% dropout) and Gaussian noise (jitter).
- **Multi-task Architecture:** Includes models for both **Classification** and **Future Trajectory Forecasting**.
- **Latent Dynamics Visualization:** Plots of vector fields and latent state evolution.

## Performance & Comparison
The NCDE model demonstrates a significant "Robustness Gap" compared to recurrent architectures like LSTMs.

| Metric | Neural CDE | LSTM |
| :--- | :---: | :---: |
| Baseline Accuracy | **95.63%** | 6.64%* |
| Accuracy with 70% Missing Data | **95.45%** | < 10% |
| Early Classification (at 40% length) | **~70%** | < 10% |

*\*LSTM baseline fails on irregular/padded sequences without significant imputation and task-specific tuning.*

## Visualizations
### 1. Robustness to Missing Data
NCDE maintains near-nominal accuracy even when 70% of the input points are removed, effectively "bridging the gaps" using learned dynamics.

### 2. Vector Field & Latent Flow
The model learns a continuous vector field $f_\theta$ that governs the evolution of the latent state $z$.
*(Insert your Vector Field Plot here)*

### 3. Future Trajectory Forecasting
The NCDE Forecaster extrapolates future pen coordinates $(x, y)$ based on partial observations with an MSE of $\sim 10^{-5}$.

## 🛠️ Implementation Details
- **Framework:** PyTorch & `torchcde`
- **Dataset:** Character Trajectories (UEA Time Series Archive)
- **Integration:** Adaptive ODE Solvers (Dormand-Prince)
- **Environment:** Developed and tested in Google Colab

## 📖 Citation
```bibtex
@article{kidger2020neuralcde,
  title={Neural Controlled Differential Equations for Irregular Time Series},
  author={Kidger, Patrick and Morrill, James and Foster, James and Lyons, Terry},
  journal={Advances in Neural Information Processing Systems},
  year={2020}
}
