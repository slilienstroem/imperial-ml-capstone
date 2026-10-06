# Engineering Log: Round 13 (Module 24)

- **Date:** October 2026
- **Data Budget:** 22 Cumulative Points -> Selection of 23rd Terminal Point
- **Execution Policy:** Terminal Horizon Pure Exploitation Override

## 1. Observations and Evaluation (Reviewing Round 12 Results)

The evaluation of the twelfth query round provided empirical validation for the structural modifications implemented in the preceding iterations:

- **Function 4 Adjustment:** Following the permanent removal of the sign-inversion multiplier from the pipeline, the Gaussian Process (GP) surrogate model aligned with the true objective landscape. Function 4 recovered from its historical minimum of -30.25431, converging at a value of -0.13948.
- **Function 7 Dimension Reduction:** Maintaining the anisotropic Automatic Relevance Determination (ARD) length-scale bounds at 1000.0 allowed the maximum marginal likelihood estimation to flatten non-contributing dimensions. Consequently, Function 7 (6D) shifted from its previous plateau of 1.96 to an evaluation score of 2.60372.
- **Plateau Consistency:** Function 5 (4D) returned to its previously observed maximum of 3747.35539, while Function 8 (8D) maintained its established coordinate plateau at a value of 9.90738.

## 2. Technical Approach for the Final Horizon (Round 13 Setup)

Because this thirteenth iteration completely exhausts the remaining query budget, a strict Terminal Horizon Policy is enforced to manage sampling risks. The acquisition configuration is transitioned entirely to exploitation:

- **Exploration Parameter Minimization:** The exploration factor has been reduced to beta = 0.001 across all eight target functions. This constrains the Upper Confidence Bound (UCB) acquisition loop to localized gradient verification around known high-performing coordinates.
- **Selective Safety Filter Deactivation:** The geometric Support Vector Machine (SVM) space filter has been deactivated for Functions 5 and 8. This ensures that the acquisition framework can evaluate the full 65,000-point Monte Carlo sampling grid near the established peaks without artificial boundary clipping.

## 3. Regularization, Constraints, and Hyperparameter Configuration

To maintain numerical stability during the final exploitation phase, internal hyperparameters were configured based on the noise profiles and dimensionality of the target functions:

- **Stochastic Noise Smoothing:** For volatile landscapes (Functions 1, 2, 4, and 6), the white-noise regularization parameter was kept at alpha = 1e-3. This prevents the Gaussian Process (GP) regressor from over-fitting to localized stochastic fluctuations. For stable landscapes (Functions 3, 5, 7, and 8), alpha was set to 1e-4 to enable precise interpolation near observed peaks.
- **Anisotropic Kernel Tuning:** The Automatic Relevance Determination (ARD) formulation remained active for high-dimensional spaces (Functions 7 and 8) with length-scale bounds set between 1e-2 and 1e3. This allows marginal likelihood maximization via L-BFGS-B to down-weight non-contributing input dimensions.
- **Space Restrictions:** The Soft-Margin Support Vector Classifier (SVC) remained active exclusively for Functions 3 and 7, using a rolling 75th percentile threshold to isolate high-yield subvolumes and prevent sampling in unpromising hypervolumes.

## 4. Analytical Assumptions and Limitations

The execution of this terminal horizon policy is guided by two operational assumptions:
1. **Local Stationarity:** The surrogate model assumes the objective function behaves predictably in the immediate geometric neighborhood of historical maxima, allowing the Matérn 5/2 kernel to compute accurate localized gradients.
2. **Grid Resolution Limits:** The 65,000-point Monte Carlo grid serves as a discrete approximation of the continuous search space. If a global optimum lies between the discrete grid intervals in high-dimensional spaces (specifically the 8D space of Function 8), it cannot be resolved by the acquisition framework.
