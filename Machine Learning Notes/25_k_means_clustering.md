# 25. K-Means Clustering

## 1. Overview
K-Means is a highly popular, iterative partition-based clustering algorithm. It seeks to divide a dataset into $K$ distinct, non-overlapping subsets (clusters) such that the total within-cluster variation is minimized.

## 2. The Objective Function
The goal is to minimize the sum of within-cluster variations across all $K$ clusters.
$$ \min_{C_1,\dots,C_K} \sum_{k=1}^{K} W(C_k) $$

The most common definition of within-cluster variation $W(C_k)$ is the sum of squared Euclidean distances between all pairs of points in the cluster, normalized by the cluster size:
$$ W(C_k) = \frac{1}{|C_k|} \sum_{i,i' \in C_k} \sum_{j=1}^{p} (x_{ij} - x_{i'j})^2 $$

Equivalent centroid form used in implementation:
$$
\sum_{k=1}^{K}\sum_{i \in C_k}\sum_{j=1}^{p}(x_{ij}-\bar{x}_{kj})^2
$$
where $\bar{x}_{kj}$ is the mean of feature $j$ inside cluster $k$.

## 3. The Algorithm (Lloyd's Algorithm)
1. **Initialization:** Randomly assign a number from $1$ to $K$ to each of the observations. These serve as initial cluster assignments.
2. **Iteration:** Repeat the following until the cluster assignments stop changing:
   - **Centroid Update:** For each of the $K$ clusters, compute the cluster *centroid*. The centroid is the vector of feature means for the observations assigned to the $k$-th cluster (this gives the algorithm its name "K-Means").
     $$ \mu_k = \frac{1}{|C_k|} \sum_{i \in C_k} x_i $$
   - **Reassignment:** Assign each observation to the cluster whose centroid is closest (using Euclidean distance).

## 4. Properties & Limitations
- **Convergence:** The algorithm is mathematically guaranteed to decrease the objective function at each step. This is because Step 2a finds constants (means) that minimize the sum-of-squared deviations, and Step 2b reallocates observations to only improve the objective. It will never increase.
- **Initialization Sensitivity:** Because it finds local optima rather than a global optimum, the final clustering depends heavily on the random initialization.
  - *Solution:* Run the algorithm multiple times (e.g., $n=10$) with different random initial configurations and explicitly select the solution where the overall objective (12.17) is smallest.
- **Choosing $K$:** The algorithm requires $K$ to be specified in advance. Selecting a "good" $K$ is non-trivial and often relies on heuristics like the "Elbow Method" or silhouette scores.

## 5. Iterative Flow Diagram

```text
 [Random Initialization]
           |
           v
 +-> [Compute Centroids (μ_k)]
 |         |
 |         v
 |   [Reassign Points to]
 |   [ Nearest μ_k      ]
 |         |
 +---------+ (Repeat until no changes)
           |
           v
    [Final Clusters]
```

## Use Cases & Limitations

**5 Use Cases (When to use):**
1. **Customer Segmentation:** Grouping customers by purchasing behavior, demographics, or engagement metrics to tailor marketing strategies.
2. **Image Compression (Color Quantization):** Reducing the color palette of an image by clustering millions of pixels into exactly $K$ distinct representative colors.
3. **Document Clustering:** Grouping a large corpus of text documents into distinct topics or themes for easier navigation and retrieval.
4. **Feature Engineering:** Using the distances from an observation to the $K$ cluster centroids as new, engineered features for a supervised machine learning model.
5. **Anomaly Detection:** Identifying outliers by finding data points that are exceptionally far from their assigned cluster centroid.

**5 Limitations (When NOT to use):**
1. **Pre-specifying $K$:** Forces the user to guess or empirically determine the "correct" number of clusters beforehand, which is often unknown in real-world data.
2. **Non-Spherical Clusters:** Assumes clusters are spherical, equally sized, and have similar densities. It fails completely on elongated, concentric, or irregularly shaped clusters (where DBSCAN is better).
3. **Outlier Sensitivity:** Because the objective function uses squared Euclidean distances, a few extreme outliers can violently drag the centroids away from the true data mass.
4. **Local Optima Guarantee:** Lloyd's algorithm is only guaranteed to find a *local* minimum. Bad random initialization can lead to a terrible clustering outcome, requiring multiple restarts.
5. **Curse of Dimensionality:** In extremely high-dimensional spaces, the Euclidean distance metric loses meaning, causing K-Means to cluster poorly without prior dimensionality reduction (like PCA).

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](24_distance_metrics.md) | [Next](26_hierarchical_clustering.md)
