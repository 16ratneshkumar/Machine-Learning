# 14. Regression Evaluation Metrics

## 1. Overview
Evaluating a regression model requires distinct metrics to measure the magnitude of prediction errors and to determine the proportion of variance successfully captured by the model.

## 2. Error Magnitude Metrics

### Residual Sum of Squares (RSS)
The absolute sum of squared differences between actual observations ($y_i$) and predictions ($\hat{y}_i$).
$$ \text{RSS} = \sum_{i=1}^{n} (y_i - \hat{y}_i)^2 $$
- **Interpretation:** A lower RSS indicates a better fit to the training data.

### Residual Standard Error (RSE)
An estimate of the standard deviation of the irreducible error $\epsilon$. It measures the average amount that the response will deviate from the true regression line.
$$ \text{RSE} = \sqrt{\frac{\text{RSS}}{n-p-1}} $$
*(Note: For simple linear regression where $p=1$, the denominator is $n-2$).*

## 3. Variance Metrics

### Total Sum of Squares (TSS)
The total variance in the response variable $Y$ before regression is performed.
$$ \text{TSS} = \sum_{i=1}^{n} (y_i - \bar{y})^2 $$

### R-Squared ($R^2$) Statistic
The proportion of variance in the dependent variable that is predictable from the independent variables.
$$ R^2 = 1 - \frac{\text{RSS}}{\text{TSS}} $$
- **Interpretation:** Bounded between 0 and 1. An $R^2$ of 1 indicates perfect prediction. High training $R^2$ does not guarantee low test error due to the risk of overfitting.

## 4. Statistical Tests

- **Individual Coefficient Test (t-statistic):** Evaluates the significance of a single predictor $X_j$.
  $$ t_j = \frac{\hat{\beta}_j}{\text{SE}(\hat{\beta}_j)} $$
- **Global Model Utility (F-statistic):** Tests if at least one predictor is statistically significant.
  $$ F = \frac{(\text{TSS} - \text{RSS})/p}{\text{RSS}/(n-p-1)} $$

## 5. Metric Relationships

```text
  [Total Variance (TSS)] = [Explained Variance] + [Unexplained Variance (RSS)]

           [R^2] = 1 - (Unexplained / Total)

      (High R^2) ----> Indicates Model fits Training Data Well
      (Low RSE)  ----> Indicates Predictions are close to Actuals
```

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](13_overfitting_and_regularization.md) | [Next](15_decision_trees.md)
