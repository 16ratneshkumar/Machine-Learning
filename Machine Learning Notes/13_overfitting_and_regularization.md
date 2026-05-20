# 13. Overfitting And Regularization

## 1. Overview
Overfitting occurs when a model is excessively complex, learning the random noise within the training data rather than the underlying signal. This results in incredibly low training error but drastically poorer performance on unseen test data (poor generalization).

## 2. Causes of Overfitting
- High model flexibility (e.g., high-degree polynomials).
- Excessively large search spaces.
- Insufficient or highly noisy training data.

## 3. Mitigation Strategies

### Subset & Stepwise Selection
Restricting the number of active features. Optimal subsets are chosen using complexity-aware metrics like validation/Cross-Validation (CV) error, AIC/BIC, or adjusted $R^2$.

### Shrinkage Methods (Regularization)
Regularization adds a penalty term to the loss function, artificially constraining the magnitude of the model coefficients. This intentionally increases model bias to significantly reduce model variance and test error.

1. **Ridge Regression (L2 Penalty):**
   Penalizes the squared magnitude of coefficients using a "shrinkage penalty". Forces coefficients to be small but rarely exactly zero.
   $$ \min \left( \text{RSS} + \lambda \sum_{j=1}^{p} \beta_j^2 \right) $$
   - **Intercept Exception:** The penalty is NOT applied to the intercept $\beta_0$. Assuming centered data, $\hat{\beta}_0 = \bar{y}$.
   - **L2 Norm Mapping:** The magnitude of shrinkage is often mapped via the $L_2$ norm: $\| \beta \|_2 = \sqrt{\sum \beta_j^2}$.
   - **Computational Speed:** Extremely fast compared to Best Subset Selection (which checks $2^p$ models). Computing ridge regression across all values of $\lambda$ simultaneously takes about the same time as a single OLS fit.

2. **Lasso Regression (L1 Penalty):**
   Penalizes the absolute magnitude of coefficients. Can force coefficients to exactly zero, effectively performing automatic feature selection.
   $$ \min \left( \text{RSS} + \lambda \sum_{j=1}^{p} |\beta_j| \right) $$

### The Necessity of Scaling
Unlike Standard Least Squares, which is **scale equivariant** (multiplying a predictor by $c$ scales its coefficient by $1/c$ without altering the model), regularized methods like Ridge are highly sensitive to scale. Therefore, predictors **must** be standardized to have a standard deviation of 1 before fitting the model:
$$ \tilde{x}_{ij} = \frac{x_{ij}}{\sqrt{\frac{1}{n}\sum_{i=1}^{n}(x_{ij} - \bar{x}_j)^2}} $$

*Note: The hyperparameter $\lambda$ controls the regularization strength and is tuned via CV. When $\lambda = 0$, the penalty has no effect (standard OLS). As $\lambda \rightarrow \infty$, coefficients approach exactly zero.*

### Other Contexts
- **Soft-Margin SVM:** The hyperparameter $C$ controls the tolerance for margin violations, serving as a regularization mechanism.
- **Neural Networks:** Rely on architectural constraints, L1/L2 weight decay, dropout, and stochastic gradient descent (SGD) early stopping to prevent over-optimization.

## 4. Bias-Variance Tradeoff
Regularization (e.g. Ridge Regression) explicitly trades a small increase in **bias** for a massive decrease in **variance**. It is particularly effective in high-variance situations where the number of predictors $p$ is almost as large as the number of samples $n$, or even when $p > n$ (where standard OLS has no unique solution).

```text
       ^ Error
       |
       |      . . (Test Error)
       |   .       .
       | .           .
       |.              .   (Overfitting Zone)
       | .               .
       +------------------- . . .  (Training Error)
       |
       +---------------------------------> Model Complexity
                (Optimal)                  (Flexibility)
```

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](12_gradient_descent.md) | [Next](14_regression_evaluation_metrics.md)
