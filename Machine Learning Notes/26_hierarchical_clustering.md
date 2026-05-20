# 26. Hierarchical Clustering

## 1. Overview
Hierarchical clustering is an agglomerative (bottom-up) approach that builds a nested tree of clusters, known as a **dendrogram**. Unlike K-Means, it does not require the user to pre-specify the number of clusters $K$ prior to execution.

## 2. The Agglomerative Algorithm
1. **Initialization:** Begin by treating every single observation as its own independent cluster (if there are $n$ observations, start with $n$ clusters).
2. **Iterative Merging:** 
   - Identify the two clusters that are most similar (i.e., have the shortest distance between them).
   - Merge these two clusters into a single new cluster.
3. **Termination:** Repeat the merging process until all observations are encapsulated within a single, massive root cluster.

## 3. Linkage Criteria
To determine the distance between two clusters (which may contain multiple points), a linkage criterion is required. Let $A$ and $B$ be two clusters:

- **Single Linkage:** The distance between the *closest* pair of points (one in $A$, one in $B$). Tends to produce long, trailing clusters (chaining) where observations are fused one at a time.
  $$ \min_{i \in A, j \in B} d(x_i, x_j) $$
- **Complete Linkage:** The distance between the *farthest* pair of points. Tends to produce compact, balanced, spherical clusters.
  $$ \max_{i \in A, j \in B} d(x_i, x_j) $$
- **Average Linkage:** The arithmetic mean of distances between all pairs of points. Also tends to yield more balanced dendrograms.
  $$ \frac{1}{|A||B|} \sum_{i \in A} \sum_{j \in B} d(x_i, x_j) $$
- **Centroid Linkage:** The distance between the calculated centroids of clusters $A$ and $B$. Often used in genomics, but suffers from a major drawback called **inversion**, whereby two clusters can fuse at a height below either of the individual clusters in the dendrogram.

## 4. The Dendrogram
The algorithm outputs a dendrogram, a tree diagram where the vertical axis represents the distance/dissimilarity at which clusters were merged. 
- **Choosing $K$:** The user can obtain a specific number of clusters by drawing a horizontal line across the dendrogram at a chosen height (cutting the tree).
- **Interpretation (Critical Rule):** The height of the merge indicates how different the two groups are; higher merges indicate joining highly dissimilar groups. **It is incorrect to draw conclusions about the similarity of two observations based on their proximity along the horizontal axis.** There are $2^{n-1}$ possible reorderings of the dendrogram branches. Similarity is exclusively determined by the vertical location where branches first fuse.
- **Nesting Limitation:** Hierarchical clustering forces clusters to be nested. If the true subgroups are not nested (e.g., the best 2-group split is by gender, but the best 3-group split is by nationality), hierarchical clustering will yield poor results compared to K-Means.

## 5. Dendrogram Structure

```text
    Dissimilarity
       ^
  High |       [---- Cluster A&B&C ----]
       |       |                       |
       |    [A&B]                      |
  Low  |    |   |                      |
       |   (A) (B)                    (C)
       +-------------------------------------> Data Points
```

## Use Cases & Limitations

**5 Use Cases (When to use):**
1. **Unknown Cluster Count:** Ideal for exploratory data analysis when you have absolutely no idea how many clusters exist ($K$ is not required upfront).
2. **Taxonomy & Evolutionary Trees:** Naturally suited for bioinformatics (genetics/phylogenetics) to map out evolutionary descent in a strict hierarchy.
3. **Visual Data Structure Discovery:** The resulting dendrogram provides a highly interpretable visual map of exactly how all subgroups relate to one another at varying levels of granularity.
4. **Small Datasets:** Highly effective on smaller datasets where the rich visual output can be comprehensively analyzed by domain experts.
5. **Document Organization:** Useful for categorizing documents where natural hierarchies exist (e.g., Science -> Physics -> Quantum Mechanics).

**5 Limitations (When NOT to use):**
1. **Massive Computational Expense:** The standard algorithm has a time complexity of $O(n^3)$ and a space complexity of $O(n^2)$, making it entirely unusable for large datasets.
2. **Irreversible Merges:** Once two clusters are merged at a lower level in the tree, they can never be separated later, even if subsequent steps reveal it was a suboptimal merge.
3. **Non-Nested True Structures:** If the true underlying data segments are not naturally nested (e.g., splitting by gender vs. splitting by country), forcing a hierarchical structure yields misleading results.
4. **Outlier Sensitivity:** Highly sensitive to noise and outliers, particularly when using "Single Linkage," which can result in severe "chaining" where outliers are appended one by one.
5. **Subjective Tree Cutting:** While you don't need to pick $K$ initially, determining where to draw the horizontal line across the dendrogram to establish the final clusters remains highly subjective.

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](25_k_means_clustering.md)
