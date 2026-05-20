# 07. Feature Scaling

## 1. Overview
Feature scaling is a critical preprocessing step required when varying magnitudes across features distort the behavior of distance-based or variance-based machine learning algorithms.

## 2. Why Scaling is Necessary
- **Distance-Based Methods:** Algorithms like k-Nearest Neighbors (k-NN), K-Means Clustering, and Support Vector Machines (SVMs) with distance-sensitive kernels rely on Euclidean distance. Without scaling, features with naturally larger ranges (e.g., salary vs. age) will disproportionately dominate the distance calculation.
- **Variance-Based Methods:** In Principal Component Analysis (PCA), variables are typically centered (mean $0$) and scaled. If left unscaled, a feature with large variance strictly due to its units will erroneously dominate the principal components.
- **Optimization:** Scaling ensures faster, more stable convergence in gradient-based optimization algorithms like Gradient Descent.

## 3. Common Scaling Techniques

### 3.1 Standardization (Z-Score Normalization)
Rescales features so that they have the properties of a standard normal distribution with a mean ($\mu$) of 0 and a standard deviation ($\sigma$) of 1.
$$ z = \frac{x - \mu}{\sigma} $$

### 3.2 Min-Max Normalization
Rescales features to a fixed range, typically $[0, 1]$.
$$ x' = \frac{x - x_{\text{min}}}{x_{\text{max}} - x_{\text{min}}} $$

## 4. Algorithmic Impact
- Ensures a fair contribution from every feature.
- Creates a better geometric space for nearest-neighbor boundaries and clustering centroids.
- Prevents numerical instabilities during model training.

## 5. Scaling Pipeline

```text
   [Raw Features]
  (Age: 20-80, Income: 30k-150k)
         |
         v
 [Scaling Operation]  <-- Standardization (z-score) or Min-Max
         |
         v
 [Scaled Features]
  (Age: 0.1-0.9, Income: 0.2-0.8)
         |
         v
 [Distance/Variance Algorithm]
```

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](06_applications_of_ml.md) | [Next](08_feature_selection_methods.md)
