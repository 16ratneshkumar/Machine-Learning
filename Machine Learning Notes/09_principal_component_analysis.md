# 09. Principal Component Analysis (PCA)

## 1. Overview
Principal Component Analysis (PCA) is an unsupervised dimensionality reduction technique that identifies a low-dimensional linear structure within a dataset, optimized to capture the maximum possible variance.

## 2. Core Mechanics
- **Unsupervised Nature:** Utilizes only the feature matrix $X_1 \dots X_p$ and ignores any target variable $Y$.
- **Applications:** Data visualization, derived variables for supervised learning, and **data imputation** (filling in missing values in a data matrix).
- **Principal Components (PCs):** The derived components are uncorrelated, orthogonal directions in the feature space.
- **First Component ($Z_1$):** The linear combination of features that maximizes the sample variance of the projected scores, subject to a unit-length loading constraint. Geometrically, the projected values $z_{11} \dots z_{n1}$ are the component scores.
- **Subsequent Components ($Z_2, Z_3, \dots$):** Maximize the remaining variance while remaining strictly orthogonal (perpendicular) to all preceding components.
- **Computation:** The optimization problem is mathematically solved via standard linear algebra techniques known as an **eigen decomposition**.

## 3. Mathematical Formulation

**First Principal Component ($Z_1$):**
$$ Z_1 = \sum_{j=1}^{p} \phi_{j1} X_j $$

**Loading Vector Constraint:**
To prevent arbitrarily large variance through massive coefficients, the squared loadings must sum to 1:
$$ \sum_{j=1}^{p} \phi_{j1}^2 = 1 $$

For components beyond the first, PCA also enforces orthogonality constraints:
$$ \sum_{j=1}^{p} \phi_{jm}\phi_{j\ell} = 0 \quad (m \neq \ell) $$
and the maximum number of non-zero principal components is:
$$ M \le \min(n-1, p) $$

## 4. Variance Explanation & Geometric Interpretation
PCA can be viewed dualistically:
1. **Variance Maximization:** Finding the direction in feature space along which the data varies the most.
2. **Minimizing Approximation Error:** The first $M$ principal components span the $M$-dimensional linear surface (hyperplane) that is closest to the $n$ observations in terms of average squared Euclidean distance. Minimizing this Mean Squared Error (MSE) is mathematically equivalent to maximizing variance.

**Proportion of Variance Explained (PVE):**
The ratio of variance captured by the $m$-th component relative to the total variance:
$$ \text{PVE}_m = \frac{\sum_{i=1}^{n} z_{im}^2}{\sum_{j=1}^{p} \sum_{i=1}^{n} x_{ij}^2} $$
*Note:* The PVE can also be expressed as $1 - \text{RSS}/\text{TSS}$, meaning it can be interpreted as the $R^2$ of the approximation for $X$ given by the first $M$ principal components.

The source variance decomposition identity is:
$$ \sum_{j=1}^{p}\sum_{i=1}^{n} x_{ij}^2 = \sum_{j=1}^{p}\sum_{i=1}^{n}\left(x_{ij} - \sum_{m=1}^{M} z_{im}\phi_{jm}\right)^2 + \sum_{m=1}^{M}\sum_{i=1}^{n} z_{im}^2 $$
which directly links reconstruction error and explained variance.

*In practice, the individual and cumulative PVE is plotted on a "Scree Plot" to visually determine the optimal number of components to retain. One typically looks for an **"elbow"** in the scree plot—the point where the proportion of variance explained by subsequent components drops off significantly.*

**Uniqueness:** Principal components are theoretically unique **up to sign flips**. Software packages may yield loading vectors with different signs because flipping the sign simply points the direction exactly 180 degrees opposite, which mathematically spans the identical line in space. The resulting score vectors will also flip, leaving the final approximation ($z_{im} \phi_{jm}$) unchanged.

## 5. Preprocessing & Visualization Tools
- **Centering:** Features must be centered (column means subtracted to equal zero) prior to PCA.
- **Scaling:** If features are measured in different units (e.g., kilograms vs. kilometers), they must be scaled (standardized to standard deviation 1) so variables with massive numeric ranges (like occurrences per 100,000 people) do not arbitrarily dominate the variance calculation. *Exception:* If variables are already measured in the exact same units (e.g., comparable expression levels for $p$ genes), you might purposefully choose *not* to scale them so their natural relative variances are preserved.
- **Biplot Visualization:** A plot that displays both the principal component scores and the principal component loading vectors simultaneously.
  - *Example (USArrests dataset):* A biplot effectively maps highly correlated variables like Murder, Assault, and Rape along PC1 (representing overall serious crime), while UrbanPop maps heavily to PC2 (urbanization). This allows easy visual clustering of states like California (high crime, high urban) versus Mississippi (low urban) or North Dakota (low crime).

## 6. PCA Transformation Flow

```text
    [Original High-Dimensional Space (X)]
                   |
             (Centering & Scaling)
                   |
        (Compute Covariance Matrix)
                   |
     (Extract Eigenvectors / Loadings: φ)
                   |
                   v
    [Orthogonal Principal Components (Z)]
     (Z_1 captures max variance, Z_2 next...)
```

## Use Cases & Limitations

**5 Use Cases (When to use):**
1. **Dimensionality Reduction:** When dealing with high-dimensional data and needing to compress the feature space while retaining most of the variance.
2. **Data Visualization:** For projecting complex datasets into 2D or 3D spaces to observe underlying patterns, clusters, or outliers.
3. **Multicollinearity Removal:** When predictors in a regression model are highly correlated, PCA can transform them into uncorrelated principal components.
4. **Noise Filtering:** Useful in signal processing to separate the principal signal (high variance) from random noise (low variance components).
5. **Feature Extraction for ML:** To speed up training times for models like SVM or Neural Networks by reducing the number of input features.

**5 Limitations (When NOT to use):**
1. **Non-Linear Relationships:** PCA assumes linear relationships between features. It performs poorly on complex manifolds or non-linear structures.
2. **Loss of Interpretability:** Principal components are linear combinations of original features, making the new variables difficult to interpret in a business context.
3. **Scale Sensitivity:** Highly sensitive to feature scaling; failure to standardize data will lead to components dominated by high-magnitude variables.
4. **Categorical Data:** Not designed for discrete or categorical variables.
5. **Supervised Tasks:** PCA ignores the target variable $Y$. It might discard components with low variance that are actually highly predictive of the target.

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](08_feature_selection_methods.md) | [Next](10_linear_regression_single_variable.md)
