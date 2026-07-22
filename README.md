# Imperial College London - MLAI Capstone Project
## Sequential Black-Box Optimization Competition (Modules 12–24)

This repository documents my engineering approach, mathematical strategies, and iterative results for the **Sequential Black-Box Optimization Challenge** as part of the Imperial College London Professional Certificate in Machine Learning & Artificial Intelligence.

### Project Overview
The objective is to maximize **eight unknown synthetic black-box functions** ranging from 2D to 8D hypervolumes. Each function simulates a high-stakes, expensive-to-evaluate industrial or scientific task like radiation source detection, drug discovery, or hyperparameter tuning where sample efficiency is paramount.

We operate under a strict **sequential data budget**, starting with 10 initial data points in Module 12 and acquiring exactly one new query coordinate per function per week, culminating in 22 total data points by the end of Module 24.

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
*This table tracks the best-observed output value (y_max) across all rounds. Lower-is-better tasks have been structurally transformed by the program into maximization problems.*

| Function | Dimension | Initial Max $y$ | Round 1 $y$ | Round 2 $y$ | Current Best $y_{max}$ |
|----------|-----------|-----------------|-------------|-------------|-----------------------|
| F1       | 2D        | *[TBD]*         | *[Pending]* |             |                       |
| F2       | 2D        | *[TBD]*         | *[Pending]* |             |                       |
| F3       | 3D        | *[TBD]*         | *[Pending]* |             |                       |
| F4       | 4D        | *[TBD]*         | *[Pending]* |             |                       |
| F5       | 4D        | *[TBD]*         | *[Pending]* |             |                       |
| F6       | 5D        | *[TBD]*         | *[Pending]* |             |                       |
| F7       | 6D        | *[TBD]*         | *[Pending]* |             |                       |
| F8       | 8D        | *[TBD]*         | *[Pending]* |             |                       |

---
👉 **[Read the Weekly Engineering Logs](./docs/logs/)**
