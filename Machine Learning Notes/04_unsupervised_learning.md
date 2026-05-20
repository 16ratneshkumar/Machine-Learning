# 04. Unsupervised Learning

## 1. Overview
Unsupervised learning operates on datasets lacking target labels, using only input observations. The primary objective is to discover hidden structures, natural subpopulations, and underlying regularities within the raw data.

## 2. Key Methodologies
### Clustering
Groups similar inputs into natural, cohesive subpopulations based on defined distance metrics.
- **Customer Segmentation:** Grouping users by demographics to support Customer Relationship Management (CRM) strategies.
- **Image Compression:** E.g., reducing a 24-bit RGB image (16 million colors) to a 6-bit image (64 main colors) by clustering shades into representative groups, trading detail for storage space.
- **Document Clustering:** Utilizing a "bag of words" model (an $N$-dimensional binary vector for $N$ lexicon words). Requires preprocessing like removing suffixes ("-s", "-ing") and uninformative stop-words (e.g., "of", "and") to avoid duplicates.
- **Bioinformatics:** Clustering genetic sequences (combinations of bases A, G, C, T) to detect recurring "motifs"—structural or functional elements analogous to words in a sentence. String alignment handles insertions, deletions, and substitutions.

### Density Estimation & Dimensionality Reduction
- **Principal Component Analysis (PCA):** Aims to preserve maximum data variance in a lower-dimensional space, distinctly different from clustering's goal of group membership discovery.
- Unsupervised techniques are frequently employed as a vital preprocessing step to simplify or structure data before applying supervised models.

## 3. Evaluation & Interpretation
- Unlike supervised learning (which has ground truth), the success of an unsupervised model is highly subjective and judged by the usefulness of the discovered structure.
- **Outlier Detection:** Elements that fail to cluster may represent anomalies or novel niche opportunities.
- **Domain Knowledge:** Essential for properly interpreting and validating the discovered patterns.

## 4. Mathematical Formulation

**Density Estimation View:**
Estimate the probability density function $p(x)$ directly from unlabeled samples.

**Cluster Assignment Rule:**
An input $x_i$ is assigned to cluster $C_k$ if its distance to the cluster centroid $\mu_k$ is minimal across all clusters:
$$ x_i \in C_k \iff \arg\min_{j} d(x_i, \mu_j) = k $$

## 5. Discovering Structure

```text
    [Unlabeled Raw Data Space]
       .     .   ..
      ...   ..      .
       .           ...

          | (Clustering Algorithm)
          v

    [Discovered Subpopulations]
       (C_1)       (C_2)
       . . .       . . .
        . .         . .
```

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](03_supervised_learning.md) | [Next](05_reinforcement_learning.md)
