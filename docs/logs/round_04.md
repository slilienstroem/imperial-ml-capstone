# Engineering Log: Round 4 (Module 15)
**Date:** August 2026  
**Data Budget:** 13+ Cumulative Points -> Submission of 14th Query Point

### 1. Performance Analysis of Round 3 Responses
The feedback array from the third execution round delivered excellent strategic validations and one great success marker:

* **Function 1 (2D):** Returned another flat response near zero. The global landscape remains entirely featuresless in this sub-volume, demanding continued boundary expansion.
* **Function 2 (2D):** Maintained its steady upward trend, rising to 0.12. This proves that scanning the vicinity of the historical baseline maximum is yielding consistent progress.
* **Functions 3, 4, and 6:** Exhibited non-linear fluctuations, with Function 4 dropping sharply to -2.32. This performance dip confirms highly complex multi-modal topographies.
* **Function 5 (4D):** Achieved an milestone, skyrocketing from 1405.55 to a yield of 1770.87. This confirms that the exploitation policy is successfully navigating the steepest ascent of the global peak.
* **Functions 7 and 8 (6D & 8D):** Retained solid plateaus at 1.10 and 9.77. Although Function 8 dropped marginally from 9.82 to 9.77, it remains firmly positioned on a high-yield local ridge.

### 2. Methodological Advancement: Support Vector Machine (SVM) Region Filtering
In alignment with the curriculum of module 14, I modified the optimization architecture to transition from a pure Gaussian Process model to a hybrid framework utilizing a Soft-Margin Support Vector Classifier (SVC). 

For functions containing non-trivial signal structures (Functions 3 through 8), a threshold was set at the 75th percentile of all historical observations to define a profitable target zone. An SVM with a Radial Basis Function (RBF) kernel and a balanced regularization constraint of C = 1.0 was trained on these labeled coordinates. 

Before evaluating the Upper Confidence Bound (UCB) acquisition function, the 50,000 Monte Carlo random sampling points were pushed through the trained SVM. The classifier drew a soft-margin hyperplane decision boundary, successfully isolating and discarding unpromising input volumes. The UCB search was restricted exclusively to coordinates validated as part of the high-probability success class, protecting the budget from drifting back into vanishing gradient zones.

### 3. Executed Query Submissions
The hybrid GP-SVM engine generated the following precise coordinates:

* **Function 1 (2D):** `0.996925-0.004402`
* **Function 2 (2D):** `0.712520-0.291144`
* **Function 3 (3D):** `0.305374-0.479312-0.494263`
* **Function 4 (4D):** `0.470343-0.362209-0.400861-0.363530`
* **Function 5 (4D):** `0.330198-0.787119-0.973775-0.981827`
* **Function 6 (5D):** `0.659010-0.363727-0.522009-0.765797-0.205309`
* **Function 7 (6D):** `0.035131-0.453463-0.253953-0.180266-0.451587-0.738522`
* **Function 8 (8D):** `0.080283-0.180448-0.064883-0.023492-0.312014-0.721983-0.376454-0.821328`

### 4. Next-Round Strategic Outlook
In Round 5, I will evaluate whether the newly introduced SVM decision boundaries reliably insulate the acquisition function from sub-optimal valleys. As the data archive expands, this hybrid filtering will allow for even narrower parameter searches, paving the way for the activation of Automatic Relevance Determination (ARD) kernels in later modules.
