# 23. Clustering Approaches

## 1. Overview
Clustering is a fundamental unsupervised learning technique aimed at discovering hidden structures within unlabelled data. The goal is to partition observations into distinct subgroups (clusters) such that data points within the same group are highly similar, while points in different groups are highly dissimilar.

## 2. Key Applications
- **Subtype Discovery:** Identifying distinct variations or heterogeneity within a population (e.g., discovering unknown subtypes of breast cancer from clinical or gene expression tissue samples).
- **Market Segmentation:** Grouping individuals based on measurements (e.g., income, occupation, rural distance) to identify subgroups more receptive to specific advertisements or product purchases.
- **Dimensionality Reduction & Summarization:** Providing a macroscopic view of complex datasets.

## 3. Comparison with PCA
Both Clustering and PCA seek to simplify data via a small number of summaries, but their mechanisms differ fundamentally. **PCA** looks to find a low-dimensional representation of the observations that explains a good fraction of the variance. **Clustering** looks to find explicit, homogeneous subgroups among the observations.

## 4. Primary Paradigms

### K-Means Clustering
- **Mechanism:** Partitions the dataset into exactly $K$ non-overlapping clusters.
- **Requirement:** The number of clusters $K$ must be pre-specified by the user.
- **Output:** A single, flat assignment of each data point to one of the $K$ clusters.

### Hierarchical Clustering
- **Mechanism:** Builds a nested, tree-like structure of clusters (a dendrogram).
- **Requirement:** Does *not* require $K$ to be fixed in advance.
- **Output:** A hierarchy where the user can choose the number of clusters post-hoc by "cutting" the tree at a desired height.

## 5. Generic Objective
Regardless of the specific algorithm, most clustering approaches seek to minimize a measure of within-cluster variation $W(C_k)$ across all clusters $C_k$:
$$ \arg\min_{C_1,\dots,C_K} \sum_{k=1}^{K} W(C_k) $$

## 6. Conceptual Flow

```text
  [Raw Unlabeled Data]
           |
           v
  (Similarity / Distance Metric applied)
           |
           v
  [Clustering Algorithm] (e.g. K-Means, Hierarchical)
           |
           v
  [Discovered Subgroups: {C_1, C_2, ..., C_K}]
```

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](22_classification_evaluation_metrics.md) | [Next](24_distance_metrics.md)
