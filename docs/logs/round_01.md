# Engineering Log: Round 1 (Module 12)
**Date:** July 2026  
**Data Budget:** 10 Initial Points $\rightarrow$ Submission of 11th Query Point

### 1. Methodological Approach & Heuristics
For the inaugural round, a uniform, highly exploratory pipeline was deployed across all eight functions. The primary objective was to partition the unmapped search spaces efficiently and mitigate data scarcity. 

* **Surrogate Model:** Gaussian Process (GP) Regression utilizing a Matérn kernel ($\nu = 2.5$) chosen for its robustness in physical and moderately rough topographies.
* **Acquisition Policy:** Upper Confidence Bound (UCB). A high exploration factor ($\beta = 3.0$) was intentionally mandated. By scaling the standard deviation ($\sigma$) three-fold, the pipeline structurally prioritized regions of maximum epistemic uncertainty - large spatial data gaps - over localized mean exploitation.
* **Acquisition Optimization:** Given the curse of dimensionality in the 5D–8D functions, standard deterministic grid searches were discarded due to exponential memory scaling. Instead, a **Monte Carlo random sampling** strategy evaluating 50,000 candidate coordinates uniformly distributed across $[0.0, 1.0]^d$ was leveraged to ensure computational tractability.

### 2. Analytical Breakthrough: Handling the "Zero Landscape"
Initial data wrangling revealed that the target space for multiple functions (most notably **Function 1**) consisted almost entirely of flat, vanishing gradients (values near or exactly $0.0$). 

During early compilation, the Maximum Likelihood Estimation (MLE) engine of the standard GP optimizer collapsed the kernel's length scale to its lower boundary ($10^{-5}$), rendering the model locally blind and causing it to default to the origin `0.000000-0.000000`. 

**Corrective Action:** The automated internal hyperparameter optimization was programmatically bypassed for this initial step. The kernel bounds were constrained (`length_scale_bounds=(0.1, 1.0)`) and the length scale fixed at a rational radius of $0.2$. This forced spatial correlation onto the flat landscape, enabling a valid space-filling acquisition rather than a numerical default crash.

### 3. Executed Query Submissions
The pipeline generated the following coordinate queries conforming to the requested format ($x_i \in [0,1]$ rounded to six decimal places, separated by hyphens):

* **Function 1 (2D):** `0.918961-0.813933`
* **Function 2 (2D):** `0.854791-0.997925`
* **Function 3 (3D):** `0.400793-0.080342-0.469810`
* **Function 4 (4D):** `0.415468-0.461440-0.442922-0.368468`
* **Function 5 (4D):** `0.278305-0.792622-0.863880-0.957522`
* **Function 6 (5D):** `0.670505-0.280118-0.572168-0.742180-0.130406`
* **Function 7 (6D):** `0.115521-0.457767-0.253082-0.105120-0.406877-0.740962`
* **Function 8 (8D):** `0.005559-0.111415-0.028853-0.097486-0.389908-0.851347-0.380352-0.730005`

### 4. Next-Round Strategic Outlook
Upon receiving the feedback metrics ($y$-values) for the 11th data point in Module 13, the policy will bifurcate based on local topological traits:
1. **Low-Dimensional/Unimodal (F1, F2, F3, F5):** If the new entry indicates exit from the zero landscape (a non-trivial signal $y > 0$), the acquisition profile will shift to **exploitation** ($\beta \rightarrow 0.5$ or switching to Expected Improvement) to climb the localized gradient of the newly discovered peak.
2. **High-Dimensional/Multi-Modal (F4, F6, F7, F8):** Due to the high density of suboptimal local maxima, exploration ($\beta \ge 2.5$) will be sustained for multiple iterations to prevent premature convergence.
