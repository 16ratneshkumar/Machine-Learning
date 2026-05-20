# 08. Feature Selection Methods

## 1. Overview
Feature selection is the process of reducing the number of input variables in a model to control model complexity, improve interpretability, and reduce the risk of overfitting.

## 2. Best Subset Selection
An exhaustive search method that evaluates all possible combinations of predictors.
- **Process:** Starts with a null model $\mathcal{M}_0$ (predicting the sample mean). It then fits all $2^p$ possible predictor subsets (e.g., $p(p-1)/2$ models containing exactly two predictors). For each size $k$, it identifies the best model $\mathcal{M}_k$ (yielding the lowest RSS or highest $R^2$).
- **Logistic Regression Variant:** Instead of ordering by RSS, it uses deviance (negative two times the maximized log-likelihood).
- **Final Selection:** Chooses the absolute best model among $\mathcal{M}_0 \dots \mathcal{M}_p$ using a validation set, or complexity-penalized metrics like cross-validation (CV), Mallows' $C_p$, BIC, or adjusted $R^2$.
- **Drawback:** Computationally prohibitive for values of $p$ greater than 40. For $p=20$, Best Subset considers 1,048,576 models, whereas Forward Stepwise considers only 211.
- **Branch-and-Bound:** Computational shortcuts exist to eliminate some choices, but they only work for least squares linear regression and still struggle as $p$ gets very large.
- **Qualitative predictors:** Categorical variables with $L$ levels are encoded using $L-1$ dummy variables; these are typically treated as a group during model specification/selection.

## 3. Stepwise Selection Methods
Computationally efficient alternatives to Best Subset Selection that evaluate far fewer models ($1 + p(p+1)/2$).

### 3.1 Forward Stepwise Selection
- **Process:** Begins with the null model (intercept only).
- Iteratively adds the single predictor that most significantly improves the model fit. Evaluates $p-k$ models at each step $k$.
- **Drawback:** Greedy approach; not guaranteed to find the globally optimal model. *Example:* If the best 1-variable model uses $X_1$, but the best 2-variable model uses $X_2$ and $X_3$, forward stepwise will fail to find it because the 2-variable model must contain $X_1$.
- **Credit Data Example:** Best subset might select 'cards' instead of 'rating' for a 4-variable model, while forward stepwise is locked into keeping 'rating' because it was selected earlier.
- **High-Dimensional Advantage:** Can be used even when $n < p$ (unlike backward stepwise), as it can construct submodels up to size $n-1$.

### 3.2 Backward Stepwise Selection
- **Process:** Begins with the full model containing all $p$ predictors.
- Iteratively removes the least useful predictor at each step.
- **Requirement:** Strictly requires the number of samples $n$ to be larger than the number of predictors $p$ ($n > p$) so the initial full least squares model can be fit.

### 3.3 Hybrid Approaches
- Variables are added sequentially similar to forward stepwise, but after adding a new variable, the method may also remove any previously added variables that no longer provide an improvement. This mimics Best Subset while retaining computational efficiency.

## 4. Evaluation Criteria
Because adding predictors *always* decreases the Training RSS and increases the standard $R^2$, the final model choice must rely on complexity-aware criteria rather than training error alone.

### Adjusted $R^2$ Formula
$$ R^2_{\text{adj}} = 1 - \frac{\text{RSS}/(n-p-1)}{\text{TSS}/(n-1)} $$
*(Where $n$ is the sample size, $p$ is the number of predictors, RSS is Residual Sum of Squares, and TSS is Total Sum of Squares).*

### Validation Set, LOOCV, and k-Fold CV
- **Validation-set approach:** split data into train/hold-out once; simple but high variance (depends on random split) and can overestimate test error because training uses fewer samples.
- **LOOCV (Leave-One-Out CV):** fit $n$ times, each time leaving one point out.
  $$ \text{CV}_{(n)} = \frac{1}{n}\sum_{i=1}^{n} \text{MSE}_i $$
  LOOCV has low bias but can have high variance and high computational cost for slow learners.
- **k-Fold CV:** split into $k$ folds (typically $k=5$ or $10$), train on $k-1$ folds, validate on the held-out fold, and average.
  $$ \text{CV}_{(k)} = \frac{1}{k}\sum_{r=1}^{k}\text{MSE}_r $$
  It is a practical bias-variance trade-off versus LOOCV.
- **Classification form:** for qualitative targets, fold error uses misclassification indicators
  $$ \text{Err}_i = I(y_i \neq \hat{y}_i) $$
  and averages these over held-out observations.
- **Bootstrap (resampling):** another source method that samples with replacement from the training set to estimate uncertainty/statistical accuracy of model estimates.

## 5. Selection Strategy Comparison

```text
                 [Feature Pool (p variables)]
                              |
        +---------------------+---------------------+
        |                     |                     |
  [Best Subset]        [Forward Stepwise]   [Backward Stepwise]
  Tests 2^p models     Adds 1 by 1          Removes 1 by 1
  Guaranteed Optimal   Greedy/Fast          Greedy/Fast
        |                     |                     |
        +---------------------+---------------------+
                              |
                              v
                 [Complexity-Aware Scoring]
                   (CV, AIC, BIC, Adj R^2)
                              |
                              v
                       [Final Model]
```

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](07_feature_scaling.md) | [Next](09_principal_component_analysis.md)
