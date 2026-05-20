# 03. Supervised Learning

## 1. Overview
Supervised learning is the paradigm of learning a mapping from input attributes to corresponding known target values, utilizing a dataset containing explicit input-output pairs.

## 2. Core Methodologies
- **Classification:** The output is a discrete class code (e.g., binary or multiclass).
  - *Credit Scoring:* Classifying applicants into low-risk vs. high-risk. A rule could be learned as: `IF income > θ1 AND savings > θ2 THEN low-risk ELSE high-risk`.
  - *Face Recognition:* A highly complex multi-class task dealing with 3D nature, differences in pose, lighting, and occlusion (e.g., glasses, beards).
  - *Medical Diagnosis:* Must handle missing inputs (due to tests being costly or time-consuming). Probabilistic outputs allow the classifier to **reject and defer the decision to a human expert** when in doubt.
  - *Speech Recognition:* Extremely difficult due to temporal sequences and varying phoneme lengths; fundamentally requires a "language model" to improve accuracy.
- **Regression:** The output is a continuous numeric value.
  - *Used Car Pricing:* Predicting the price based on attributes (brand, year, mileage) using linear formulations like $y = wx + w0$ or higher-order polynomials.
  - *Autonomous Navigation:* Outputting the continuous steering angle for a vehicle using inputs from a video camera and GPS.
  - *Response Surface Design:* Regressions can be used to optimize functions, such as finding the optimal temperature and time settings to maximize coffee roasting quality.

## 3. Model Dependencies
- **Data Representation:** Algorithms rely on representative training data. Missing values must be explicitly handled.
- **Data Integrity:** Quality heavily depends on ensuring that future data remains consistent with the training distribution.

## 4. Mathematical Formulation

The supervised learning mapping can be defined as a function bridging the feature space $\mathcal{X}$ and the target space $\mathcal{Y}$:

$$ f: \mathcal{X} \rightarrow \mathcal{Y} $$

Where the prediction $\hat{y}$ for a given input $x$ is:
$$ \hat{y} = f(x | \theta) $$

*Where $\theta$ represents the optimized parameters derived from the training pairs $(x_i, y_i)$.*

## 5. Supervised Architecture

```text
       [Training Data: (X, Y)]
                 |
                 v
           [Algorithm] <---- (Loss Minimization)
                 |
                 v
       [Learned Function: f(X)]
                 |
                 v
 [New Input, X'] ---> [ f(X') ] ---> [Prediction, Y']
```

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](02_key_elements_of_ml.md) | [Next](04_unsupervised_learning.md)
