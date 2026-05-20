# 21. Support Vector Machine (SVM)

## 1. Overview
The Support Vector Machine (SVM) is a powerful, mathematically rigorous classifier that constructs hyperplanes in a multidimensional space to separate different classes. It extends linear margin classifiers to handle noisy and non-linear boundaries.

## 2. Linear Hyperplanes & Margins
A hyperplane in a $p$-dimensional space is defined as:
$$ \beta_0 + \beta_1 X_1 + \dots + \beta_p X_p = 0 $$
$$ \beta_0 + \beta^T x = 0 $$

- **Maximal Margin Classifier:** For perfectly separable data, this finds the hyperplane that is farthest from the closest training observations.
- **Support Vectors:** The specific training observations that lie exactly on the edge of the margin. The entire boundary is dictated *only* by these support vectors; moving or deleting other points has zero effect.

## 3. Support Vector Classifier (Soft Margin)
Real-world data is rarely perfectly separable. The Soft Margin classifier introduces slack variables ($\epsilon_i$) to allow some observations to be on the wrong side of the margin or hyperplane.

- **The $C$ Hyperparameter:** Acts as a budget for margin violations.
  - **Large $C$:** High tolerance for violations. Results in a wider margin, allowing more support vectors (Higher Bias, Lower Variance).
  - **Small $C$:** Low tolerance. Fits the training data very rigidly (Lower Bias, Higher Variance risk).

**Optimization form:**
$$
\max_{\beta_0,\beta_1,\dots,\beta_p,M,\epsilon_1,\dots,\epsilon_n} M
$$
subject to:
$$
\sum_{j=1}^{p}\beta_j^2 = 1,\quad
y_i(\beta_0 + \beta^T x_i) \ge M(1-\epsilon_i),\quad
\epsilon_i \ge 0,\quad
\sum_{i=1}^{n}\epsilon_i \le C
$$
This explicitly shows margin maximization with bounded total violations.

## 4. The "Kernel Trick" (Non-Linear SVM)
To handle non-linear boundaries, SVM maps the data into a higher-dimensional space where a linear hyperplane can separate the classes. Instead of actually computing the computationally explosive feature expansion, it simply replaces inner dot-products with a **Kernel Function** $K(x_i, x_j)$.

**SVM Decision Rule:**
$$ f(x) = \beta_0 + \sum_{i \in S} \alpha_i K(x, x_i) $$
*(Where $S$ is the set of support vectors).*

- **Linear kernel equivalence:** The support vector classifier is an SVM with polynomial kernel degree $d=1$.
- **Radial kernel locality:** For RBF kernels, far-away training observations contribute almost nothing to $f(x)$, so prediction is dominated by nearby points.
- **Computational advantage:** Kernel methods avoid explicit construction of huge (or even infinite-dimensional) feature maps and only require pairwise kernel evaluations.

### Common Kernels
1. **Polynomial Kernel:**
   $$ K = (1 + \sum_{j} x_{ij} x_{i'j})^d $$
2. **Radial Basis Function (RBF) Kernel:** 
   Creates localized, non-linear boundaries based on proximity.
   $$ K = \exp\left(-\gamma \sum_{j} (x_{ij} - x_{i'j})^2\right) $$

### Multiclass Extensions
SVM is fundamentally binary; for $K$ classes, source material uses:
- **One-vs-One:** Train $K(K-1)/2$ binary classifiers.
- **One-vs-All:** Train $K$ binary classifiers.
- In one-vs-one, final class labels are typically chosen by majority voting across pairwise classifiers.

## 5. Margin Architecture

```text
        o   o      |      x
            o      |    x
   (Class -1)  [Margin]   (Class +1)
             o...  |  ...x
               SV  |  SV
                   |
            (Hyperplane: β^T x + β_0 = 0)
```

## Use Cases & Limitations

**5 Use Cases (When to use):**
1. **High-Dimensional Spaces:** Exceptionally effective when the number of features ($p$) is strictly greater than the number of samples ($n$), common in text classification and bioinformatics (e.g., gene expression data).
2. **Complex Non-Linear Boundaries:** Using the "Kernel Trick" (especially RBF kernels), it can elegantly model highly non-linear decision surfaces without exploding computational costs.
3. **Robustness to Overfitting:** The maximization of the margin provides strong theoretical guarantees against overfitting, especially in high dimensions.
4. **Memory Efficiency:** After training, the model only needs to store the Support Vectors in memory, not the entire dataset, to make future predictions.
5. **Outlier Detection:** The One-Class SVM variation is a premier algorithmic choice for unsupervised anomaly and novelty detection.

**5 Limitations (When NOT to use):**
1. **Massive Datasets:** Training time scales roughly between $O(n^2)$ and $O(n^3)$. It becomes computationally unfeasible for datasets with millions of rows.
2. **Noisy, Overlapping Classes:** Struggles significantly when classes are highly overlapping or data is extremely noisy, as the margin concept breaks down.
3. **No Probabilistic Output:** SVMs output a hard class label based on geometric distance, not a probability. Extracting probabilities requires expensive post-processing (like Platt scaling).
4. **Hyperparameter Tuning Cost:** Finding the optimal combination of the $C$ penalty parameter and the Kernel parameters (like $\gamma$) usually requires exhaustive grid searches.
5. **Lack of Transparency:** While linear SVMs are interpretable, non-linear Kernel SVMs are opaque "black boxes," making it hard to explain the influence of individual features.

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](20_multilayer_perceptron_and_neural_networks.md) | [Next](22_classification_evaluation_metrics.md)
