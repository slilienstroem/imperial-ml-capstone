# Imperial College London - MLAI Capstone Project
## Sequential Black-Box Optimization Competition (Modules 12–24)

This repository documents my engineering approach, mathematical strategies, and iterative results for the **Sequential Black-Box Optimization Challenge** as part of the Imperial College London Professional Certificate in Machine Learning & Artificial Intelligence.

### Project Overview
The objective is to maximize **eight unknown synthetic black-box functions** ranging from 2D to 8D hypervolumes. Each function simulates a high-stakes, expensive-to-evaluate industrial or scientific task like radiation source detection, drug discovery, or hyperparameter tuning where sample efficiency is paramount.

We operate under a **sequential data budget**, starting with 10 initial data points in Module 12 and acquiring one new query coordinate per function per week, culminating in 22 total data points by the end of Module 24.

### The 8 Black-Box Challenges
* **Function 1 (2D):** Radiation Field Source Detection (Vanishing gradients/Sparsity challenge).
* **Function 2 (2D):** Noisy ML Log-Likelihood Optimization (Stochastic/Local maxima challenge).
* **Function 3 (3D):** Drug Discovery/Side-Effect Minimization (Constrained input/Output-transformed maximization).
* **Function 4 (4D):** E-Commerce Product Placement (Expensive evaluation/Dynamic system simulation).
* **Function 5 (4D):** Chemical Factory Yield Optimization (Smooth/Unimodal baseline tracking).
* **Function 6 (5D):** Cake Recipe Composition / Expert Taster Metric (Multi-criteria negative score maximization).
* **Function 7 (6D):** ML Model Hyperparameter Tuning (Highly non-linear validation score landscape).
* **Function 8 (8D):** High-Dimensional Deep Learning Architecture Calibration (Curse of dimensionality challenge).

### Project Layout
```text
├── initial_data/          # Structured by function_1/ to function_8/ containing .npy files
├── Capstone_Master_Code.ipynb # Main automated orchestration pipeline
├── docs/
│   └── logs/              # Weekly Engineering Logs (Round-by-Round Breakdown)
│       └── round_01.md    # Module 12: Initial Exploration Strategy
└── README.md              # Project executive summary
```

### Cumulative Results Tracker
*This table tracks the baseline maxima and the absolute best-observed output value like y_max achieved across all sequential optimization rounds.*

| Function | Dimension | Baseline Max $y$ | Round 1 Feedback ($y$) | Round 2 Feedback ($y$) | Round 3 Feedback ($y$) | Current Best $y_{max}$ | Target Type |
|----------|-----------|------------------|------------------------|------------------------|------------------------|-----------------------|-------------|
| **F1**   | 2D        | 0.00             | 1.59e-83               | -4.17e-157             | 1.18e-216              | **0.00**              | Maximization |
| **F2**   | 2D        | 0.61             | -0.04                  | 0.05                   | 0.12                   | **0.61**              | Maximization |
| **F3**   | 3D        | -0.03            | -0.08                  | -0.01                  | -0.02                  | **-0.01**             | Maximization |
| **F4**   | 4D        | -0.42            | -0.42                  | -0.95                  | -2.32                  | **-0.42**             | Maximization |
| **F5**   | 4D        | *[Low]*          | 1245.62                | 1405.55                | 1770.87                | **1770.87** 🔥        | Maximization |
| **F6**   | 5D        | -0.31            | -0.31                  | -0.55                  | -0.53                  | **-0.31**             | Maximization |
| **F7**   | 6D        | 1.36             | 1.25                   | 1.35                   | 1.10                   | **1.36**              | Maximization |
| **F8**   | 8D        | 9.67             | 9.67                   | 9.82                   | 9.77                   | **9.82**              | Maximization |

---
👉 **[Read the Weekly Engineering Logs](./docs/logs/)**
