# Imperial ML Capstone Project: Black-Box Optimisation Challenge

## Section 1: Project Overview
This capstone project focuses on Black-Box Optimisation (BBO) using sequential design strategies. The overarching goal is to locate the global maxima of eight distinct, hidden target functions without possessing analytical knowledge of their mathematical structures, gradients, or operational landscapes. 

In real-world machine learning, BBO is a critical methodology for automated hyperparameter tuning (such as optimizing deep learning architectures), chemical compound design, complex simulation engineering, and pricing algorithms where assessing a configuration is highly expensive or time-consuming. 

Mastering these sequential decision-making frameworks under epistemic uncertainty provides a vital skill set for my data science career. It directly mirrors industrial challenges where deployment decisions must be made strategically using sparse, noisy, and costly data feeds, paving the way for designing efficient automated machine learning (AutoML) pipelines.

## Section 2: Inputs and Outputs
The optimization pipeline interacts with the black-box engine through a standardized input-output protocol. For each of the eight separate tasks, the machine learning architecture receives and processes a historical numpy array database containing cumulative inputs and corresponding outputs.

*   **Inputs:** A continuous, bounded coordinate vector within a hypercubic unit space. Dimensions vary across functions from 2D up to 8D. Each coordinate must strictly fall within the constraints of 0.000000 to 1.000000. For submission, the query format requires a single hyphen-separated string rounded precisely to six decimal places (for example, `0.320637-0.791333-0.947010-0.960370` for a 4D task).
*   **Outputs:** A single scalar response value representing the objective performance signal returned by the black-box engine after a sequential processing delay. This signal is unnormalized and scales uniquely for each task (for example, floating-point metrics near zero for F1, or scaling above 2000.00 for industrial yield simulations in F5).

*Note on Data Hosting:* In strict accordance with the Capstone Project FAQs, the raw numerical .npy datasets (initial historical baselines and cumulative array updates) are not hosted directly within this public GitHub repository. The underlying data source is securely stored and maintained locally, while the structural metadata, formats, and tracking limits are fully defined within this documentation.

## Section 3: Challenge Objectives
The core objective is to maximize the performance output across all eight distinct black-box functions. Tasks historically configured for minimization have been structurally transformed by my pipeline into maximization problems to ensure structural consistency. 

The strategy must rigorously operate within the following systemic constraints:
1.  **Strict Query Budget:** A limitation of exactly one query submission per function per week over a multi-week horizon.
2.  **Evaluation Latency:** High response delay, preventing instantaneous feedback loop adjustments.
3.  **Agnostic Environments:** Completely unknown function topographies, requiring the model to robustly handle diverse landscapes, varying noise levels, and non-uniform heteroscedasticity.

## Section 4: Technical Approach
My technical architecture evolved from a uniform baseline exploration to a highly customized, two-stage hybrid machine learning pipeline:

*   **Surrogate Modeling:** I implement a Bayesian optimization framework utilizing a Gaussian Process (GP) regressor with an isotropic Matern kernel (length scale fixed at 0.2) to mathematically model the unknown response surfaces while securing numerical stability in flat gradient regions.
*   **Geometric Filtering (SVM):** To isolate productive regions, a Soft-Margin Support Vector Machine (SVC with an RBF kernel and C=1.0) is trained dynamically on historical data binarized by a 75th percentile threshold. The SVM draws a non-linear decision boundary, creating a safety enclave that discards unpromising coordinate volumes.
*   **Exploration versus Exploitation Balance:** The UCB acquisition function is controlled on a strictly function-by-function basis. For high-performing signals like Function 5 (yield at 2154.69), beta is collapsed to 0.05 (Exploitation) to accelerate local gradient ascent. For flat or declining regions like Functions 1 and 4, beta is elevated to 3.0 (Sustained Exploration) to systematically scan the boundaries of the hypercube using a 50,000-point Monte Carlo sampling procedure.

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
├── initial_data/              # Local data storage (Structured by function_1/ to function_8/, excluded via .gitignore)
├── models/
│   └── Capstone_Master_Code.ipynb # Main automated machine learning orchestration pipeline
├── docs/
│   └── logs/                  # Weekly Engineering Logs (Sequential round-by-round progress)
│       ├── round_01.md        # Module 12: Initial Uniform Exploration Strategy
│       ├── round_02.md        # Module 13: Differentiated Acquisition Policies
│       ├── round_03.md        # Module 14: Exploitation Search Loop (F5 Peak Exploration)
│       ├── round_04.md        # Module 15: Hybrid GP-SVM Support Vector Region Filtering
│       ├── round_05.md        # Module 16: Exploitation Fine-Tuning and Peak Verification
│       ├── round_06.md        # Module 17: Automatic Relevance Determination (ARD) Tuning
│       └── round_07.md        # Module 18: Stratified Exploration Weights and Active Optimization
├── .gitignore                 # Technical safeguard to prevent public hosting of raw .npy datasets
└── README.md                  # Project executive summary and comprehensive portfolio overview
```

### Cumulative Results Tracker
*This table tracks the baseline maxima and the absolute best-observed output value like y_max achieved across all sequential optimization rounds.*

| Function | Dimension | Baseline Max y | Round 1 Feedback (y) | Round 2 Feedback (y) | Round 3 Feedback (y) | Round 4 Feedback (y) | Round 5 Feedback (y) | Round 6 Feedback (y) | Current Best y_max | Target Type |
|----------|-----------|----------------|----------------------|----------------------|----------------------|----------------------|----------------------|----------------------|--------------------|-------------|
| **F1**   | 2D        | 0.00           | 1.59e-83             | -4.17e-157           | 1.18e-216            | 0.00                 | 2.07e-169            | 6.87e-246            | **0.00**           | Maximization |
| **F2**   | 2D        | 0.61           | -0.04                | 0.05                 | 0.12                 | 0.53                 | -0.05                | -0.08                | **0.61**           | Maximization |
| **F3**   | 3D        | -0.03          | -0.08                | -0.01                | -0.02                | -0.00                | -0.02                | -0.02                | **-0.00**          | Maximization |
| **F4**   | 4D        | -0.42          | -0.42                | -0.95                | -2.32                | -0.69                | -2.13                | -4.32                | **-0.42**          | Maximization |
| **F5**   | 4D        | *[Low]*        | 1245.62              | 1405.55              | 1770.87              | 2154.69              | 2229.18              | 2767.84              | **2767.84** 🔥     | Maximization |
| **F6**   | 5D        | -0.31          | -0.31                | -0.55                | -0.53                | -0.51                | -0.36                | -0.43                | **-0.31**          | Maximization |
| **F7**   | 6D        | 1.36           | 1.25                 | 1.35                 | 1.10                 | 1.20                 | 1.44                 | 1.18                 | **1.44** 🚀        | Maximization |
| **F8**   | 8D        | 9.67           | 9.67                 | 9.82                 | 9.77                 | 9.73                 | 9.64                 | 9.67                 | **9.82**           | Maximization |

### Cumulative Results Tracker
*This table tracks the baseline maxima and the absolute best-observed output value like y_max achieved across all sequential optimization rounds.*

| Function | Dimension | Baseline Max y | Round 1 Feedback (y) | Round 2 Feedback (y) | Round 3 Feedback (y) | Round 4 Feedback (y) | Round 5 Feedback (y) | Current Best y_max | Target Type |
|----------|-----------|----------------|----------------------|----------------------|----------------------|----------------------|----------------------|--------------------|-------------|
| **F1**   | 2D        | 0.00           | 1.59e-83             | -4.17e-157           | 1.18e-216            | 0.00                 | 2.07e-169            | **0.00**           | Maximization |
| **F2**   | 2D        | 0.61           | -0.04                | 0.05                 | 0.12                 | 0.53                 | -0.05                | **0.61**           | Maximization |
| **F3**   | 3D        | -0.03          | -0.08                | -0.01                | -0.02                | -0.00                | -0.02                | **-0.00**          | Maximization |
| **F4**   | 4D        | -0.42          | -0.42                | -0.95                | -2.32                | -0.69                | -2.13                | **-0.42**          | Maximization |
| **F5**   | 4D        | *[Low]*        | 1245.62              | 1405.55              | 1770.87              | 2154.69              | 2229.18              | **2229.18** 🔥     | Maximization |
| **F6**   | 5D        | -0.31          | -0.31                | -0.55                | -0.53                | -0.51                | -0.36                | **-0.31**          | Maximization |
| **F7**   | 6D        | 1.36           | 1.25                 | 1.35                 | 1.10                 | 1.20                 | 1.44                 | **1.44** 🚀        | Maximization |
| **F8**   | 8D        | 9.67           | 9.67                 | 9.82                 | 9.77                 | 9.73                 | 9.64                 | **9.82**           | Maximization |

---
👉 **[Read the Weekly Engineering Logs](./docs/logs/)**
