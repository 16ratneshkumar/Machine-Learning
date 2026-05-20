# 24. Distance Metrics

## 1. Overview
In machine learning algorithms that rely on spatial relationships (like k-NN, K-Means, and SVM kernels), the choice of distance or similarity metric is foundational. The metric mathematically defines what it means for two data points to be "close" or "similar," directly dictating the algorithm's behavior and the resulting boundaries/clusters.

## 2. Common Distance Metrics

### Euclidean Distance (L2 Norm)
The straight-line distance between two points in Euclidean space. It is the most standard metric used in k-NN and K-Means.
$$ d(x, y) = \sqrt{\sum_{j=1}^{p} (x_j - y_j)^2} $$

### Manhattan Distance (L1 Norm)
The sum of absolute differences across all dimensions (often called city-block distance). More robust to heavy outliers than Euclidean distance.
$$ d(x, y) = \sum_{j=1}^{p} |x_j - y_j| $$

### Cosine Similarity & Correlation-Based Distance
Measures the orientation or correlation rather than magnitude. It considers two observations similar if their features are highly correlated, focusing on the *shapes* of observation profiles rather than their magnitudes.
- *Example (Online Shopping):* If we cluster shoppers based on item purchase counts using Euclidean distance, infrequent shoppers cluster together regardless of preference. Using correlation-based distance, shoppers who prefer the exact same items (e.g., items A and B) cluster together, even if one shopper buys 10x more volume than the other.
$$ \text{Similarity}(x, y) = \frac{x \cdot y}{||x|| ||y||} $$

## 3. Algorithmic Impact
- **k-NN:** Relies directly on the distance metric to select the nearest neighbors.
- **K-Means:** The objective function explicitly minimizes the squared Euclidean distance between points and their assigned cluster centroid.
- **SVM (RBF Kernel):** Uses squared Euclidean distance within its exponential function to define non-linear proximity.

## 4. The Importance of Feature Scaling
Distance metrics are highly sensitive to the scale of the features.
- *Example:* A high-frequency purchase like "socks" (bought 10 times a year) will mathematically dominate the distance calculation over a low-frequency, high-value purchase like a "computer" (bought once every 5 years), masking true underlying preferences.
**Requirement:** Variables should generally be scaled to have a standard deviation of 1 before computing distances, ensuring all variables (whether measured in centimeters or kilometers, or socks vs. computers) contribute equitably.

## 5. Selecting a Metric
- The "wrong" metric can unnaturally split or merge semantic groups.
- The choice must align with the domain semantics of the data.
- Validation is performed empirically by checking the quality of the downstream classification or clustering results.

## 6. Geometric Interpretation

```text
       y
       ^
       |    * (Point B)
       |   /| 
       |  / |  <-- Manhattan Path (Grid)
       | /  |
       |/   |
       *----*-----------------> x
    (Point A)
    
    Euclidean = Straight diagonal line
    Manhattan = Horizontal + Vertical edges
```

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](23_clustering_approaches.md) | [Next](25_k_means_clustering.md)
