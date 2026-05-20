# 18. K-Nearest Neighbor (k-NN)

## 1. Overview
The k-Nearest Neighbor (k-NN) algorithm is an instance-based, "lazy" learning method. Unlike "eager" learning methods that construct a general, parametric mathematical model at training time, lazy learning simply stores the presented training data. All computation is deferred until query time, where a local approximation of the target function is constructed in the neighborhood of the new query.
- **Advantage:** Highly effective when the target function is complex but can be described by a collection of less complex local approximations.
- **Disadvantage:** High computational cost at classification time.
- **Case-Based Reasoning:** A symbolic variation of instance-based learning used in tasks like legal case reasoning, help-desk troubleshooting, and engineering scheduling.

## 2. Core Mechanism
Examples are represented as points in a multi-dimensional feature space. 
- **Distance Metric:** Similarity is most commonly calculated using Euclidean distance between feature vectors $x_i$ and $x_j$:
  $$ d(x_i, x_j) = \sqrt{\sum_{r=1}^{p} (a_r(x_i) - a_r(x_j))^2} $$
- **Classification:** Predicts the majority (mode) class among the $k$ nearest training points.
  $$ \hat{y} = \text{mode}(\{y_{(1)}, \dots, y_{(k)}\}) $$
- **Regression:** Predicts the mean (or weighted mean) of the $k$ nearest neighbors:
  $$ \hat{f}(x_q) = \frac{\sum_{i=1}^{k} f(x_i)}{k} $$

## 3. The Parameter $k$
- **$k=1$:** The algorithm assigns the exact label of the single closest neighbor. The decision boundaries form highly localized, jagged **Voronoi diagrams** where the decision surface is a combination of convex polyhedra surrounding each training example (low bias, high variance).
- **Larger $k$:** Smoothes the decision boundaries, increasing robustness to noisy outliers (higher bias, lower variance). We can smooth out the impact of isolated noisy training examples by taking the weighted average of the $k$ neighbors.

## 4. Distance-Weighted k-NN
Instead of equal voting, neighbors can be weighted inversely proportional to their distance. Closer neighbors exert a stronger influence on the final prediction, allowing the algorithm to incorporate global data while heavily favoring local evidence.
- **Weight Formula:** $w_i = \frac{1}{d(x_q, x_i)^2}$ (avoiding division by zero by assigning $\hat{f}(x_q) = f(x_i)$ if $d(x_q, x_i) = 0$).
- **Weighted Regression:**
  $$ \hat{f}(x_q) = \frac{\sum_{i=1}^{k} w_i f(x_i)}{\sum_{i=1}^{k} w_i} $$
- **Shepard's Method:** A global variant of distance-weighted k-NN where *all* training examples are considered ($k=n$). It runs slower but avoids thresholding neighbors.
- General inverse-distance weighting form from source:
  $$ w_i = \frac{1}{d(x_q, x_i)^q}, \quad q \ge 0 $$

## 5. Vulnerabilities, Indexing, & Preprocessing
Because k-NN relies entirely on spatial distance:
- **Feature Scaling:** Absolutely critical. Unscaled features with massive numeric ranges (e.g., salary in hundreds of thousands) will entirely dominate the distance calculation over small-range features (e.g., age).
- **Irrelevant Attributes & Curse of Dimensionality:** The inclusion of noise or completely irrelevant features corrupts the distance metric. If an instance has 20 attributes but only 2 are relevant, the distance calculation is entirely dominated by the 18 irrelevant attributes, masking true similarity.
  - *Stretching Axes:* Weight each attribute differently by multiplying the $j$-th axis by a factor $z_j$. The factors $z_1 \dots z_n$ are chosen automatically via cross-validation to minimize error.
  - *Attribute Elimination:* Set $z_j = 0$ for completely irrelevant features (e.g., via leave-one-out cross-validation).
- **Efficient Indexing (kd-trees):** Exhaustive distance calculation at query time is computationally heavy. To accelerate search, stored training instances are organized at the leaves of a **kd-tree**, sorting nearby instances into the same or neighboring nodes. internal nodes test selected attributes of the query $x_q$ to route it to the relevant leaf.

## 6. Nearest Neighbor Geometry

```text
      [Class A]             [Class B]
          *                    ^
          *   (x_new)          ^
                  ?            ^
          *                    ^
                   
      For k=3: Finds 2 '*' and 1 '^' near '?'
      Prediction: Class A (*) wins majority vote.
```

## Use Cases & Limitations

**5 Use Cases (When to use):**
1. **Pattern Recognition & OCR:** Excellent for basic image recognition tasks (like classifying handwritten digits) where similar images are clustered closely in pixel-space.
2. **Recommender Systems:** Used in user-based collaborative filtering to find "users similar to you" to recommend movies, products, or music.
3. **Missing Data Imputation:** A standard technique to fill in missing dataset values by calculating the average of the $k$ nearest known neighbors.
4. **Non-Linear Decision Boundaries:** Ideal when the mathematical relationship between features and the target is highly irregular and cannot be captured by linear models.
5. **Concept Drift Tolerance:** Because it is a "lazy" learner that doesn't pre-compile a static model, it can instantly adapt to new data appended to the database without retraining.

**5 Limitations (When NOT to use):**
1. **High Latency at Inference:** The model is extremely slow at prediction time, as it must compute the distance to every single training example for every new query.
2. **The Curse of Dimensionality:** Performance severely degrades in high-dimensional spaces because the concept of "distance" becomes meaningless (all points become roughly equidistant).
3. **Extreme Sensitivity to Scaling:** If features are not strictly normalized (e.g., standardizing age vs. salary), large-scale features will completely dominate the distance metric.
4. **Memory Intensive:** Requires the entire training dataset to be kept in memory at all times, making it impractical for massive datasets.
5. **Outlier Vulnerability:** Very sensitive to noisy data and outliers, especially when $k$ is small, as isolated bad data points will heavily skew local predictions.

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](17_logistic_regression.md) | [Next](19_perceptron.md)
