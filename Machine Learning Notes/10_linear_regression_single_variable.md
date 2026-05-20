# 10. Linear Regression (Single Variable)

## 1. Overview
Simple Linear Regression assumes a linear relationship between a single predictor variable $X$ and a continuous quantitative response variable $Y$. The goal is to estimate the coefficients that minimize the residual error between the predictions and the actual data.

## 2. The Linear Model
**Theoretical Stochastic Form:**
$$ Y = \beta_0 + \beta_1 X + \epsilon $$
- $\beta_0$: Intercept (expected response when $X=0$).
- $\beta_1$: Slope (average change in $Y$ for a one-unit increase in $X$).
- $\epsilon$: The irreducible error term (mean zero, independent of $X$). This is a "catch-all" for what we miss: non-linearity, unmeasured variables, and measurement error.

**Residual Error ($e_i$):**
The difference between the actual observed value $y_i$ and the predicted value $\hat{y}_i$:
$$ e_i = y_i - \hat{y}_i $$

## 3. Ordinary Least Squares (OLS) Estimation
The objective is to minimize the **Residual Sum of Squares (RSS)**:
$$ \text{RSS} = \sum_{i=1}^{n} (y_i - \hat{\beta}_0 - \hat{\beta}_1 x_i)^2 $$

Using calculus, the closed-form solutions for the coefficients are:
$$ \hat{\beta}_1 = \frac{\sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})}{\sum_{i=1}^{n} (x_i - \bar{x})^2} $$
$$ \hat{\beta}_0 = \bar{y} - \hat{\beta}_1 \bar{x} $$
*(Where $\bar{y}$ and $\bar{x}$ are the sample means).*

**Population vs. Least Squares Line:**
- **Population Regression Line:** The unobserved, true relationship $f(X)$.
- **Least Squares Line:** The estimate calculated from the sample data.
- *Analogy:* This is identical to estimating an unobserved population mean $\mu$ using a sample mean $\hat{\mu} = \bar{y}$. The OLS estimators are **unbiased**, meaning that if we averaged the estimates over a huge number of data sets, they would perfectly equal the true population parameters.

## 4. Statistical Inference & Evaluation
- **Standard Errors:** The accuracy of the estimates depends on their standard errors. $\text{SE}(\hat{\beta}_1)$ is smaller when the $x_i$ values are more spread out (providing more leverage to estimate the slope).
  $$ \text{SE}(\hat{\beta}_0)^2 = \sigma^2 \left[ \frac{1}{n} + \frac{\bar{x}^2}{\sum_{i=1}^{n} (x_i - \bar{x})^2} \right] $$
  $$ \text{SE}(\hat{\beta}_1)^2 = \frac{\sigma^2}{\sum_{i=1}^{n} (x_i - \bar{x})^2} $$
- **Residual Standard Error (RSE):** An estimate of the standard deviation of $\epsilon$ (noted as $\sigma$ in the equations above), representing the average amount the response will deviate from the true regression line.
  $$ \text{RSE} = \sqrt{\frac{\text{RSS}}{n-2}} $$
  *Example:* In a Sales vs. TV Advertising model, an RSE of 3.26 means predictions are off by ~3,260 units on average.
- **$R^2$ Statistic:** Measures the proportion of variability explained.
  $$ R^2 = \frac{\text{TSS} - \text{RSS}}{\text{TSS}} = 1 - \frac{\text{RSS}}{\text{TSS}} $$
  - **Context Dependency:** In physics, a good $R^2$ is extremely close to 1. In biology, psychology, or marketing, an $R^2$ well below 0.1 might be highly realistic due to massive unmeasured variation.
  - **Correlation Equivalence:** In simple linear regression, $R^2 = r^2$, where $r$ is the Pearson correlation coefficient between $X$ and $Y$.
- **Confidence Intervals:** A 95% confidence interval for the slope can be approximated as:
  $$ \hat{\beta}_1 \pm 2 \cdot \text{SE}(\hat{\beta}_1) $$
- **Hypothesis Testing:**
  - Null Hypothesis ($H_0$): $\beta_1 = 0$ (No relationship exists between $X$ and $Y$).
  - Evaluated using a **t-statistic** (number of standard deviations $\hat{\beta}_1$ is away from 0):
    $$ t = \frac{\hat{\beta}_1}{\text{SE}(\hat{\beta}_1)} $$
  - A small p-value (typically $< 0.05$) indicates strong evidence to reject $H_0$, confirming a statistically significant association.

## 5. Regression Line Fitting

```text
    Y
    ^
    |       * (y_i)
    |       | e_i (Residual)
    |     .-+-. (y_hat_i)
    |  .-'
    .-'   [ Regression Line: y = β_0 + β_1*x ]
    |
    +----------------------------------------> X
```

## Use Cases & Limitations

**5 Use Cases (When to use):**
1. **Trend Analysis:** Ideal for predicting continuous numerical values over time, such as future sales based on historical data.
2. **Understanding Simple Relationships:** When you need to understand the fundamental relationship and correlation between exactly one predictor and a target variable (e.g., studying the effect of hours studied on exam scores).
3. **Baseline Modeling:** Excellent as an initial baseline model to benchmark the performance of more complex algorithms.
4. **Impact Assessment:** Useful in economics and business to quantify the impact of a specific independent variable on a dependent variable.
5. **Risk Assessment:** Used in finance to calculate the beta of a stock (its volatility relative to the overall market).

**5 Limitations (When NOT to use):**
1. **Non-Linear Data:** Performs poorly if the underlying relationship between $X$ and $Y$ is non-linear (e.g., exponential growth).
2. **Outlier Sensitivity:** Highly susceptible to outliers, which can drastically skew the Ordinary Least Squares (OLS) regression line.
3. **Multivariate Complexity:** Inadequate for real-world scenarios where the target variable depends on multiple interacting features.
4. **Heteroscedasticity:** Assumes constant variance of errors; if the variance of residuals changes over time or across values of $X$, the predictions become unreliable.
5. **Categorical Targets:** Cannot be used for classification problems where the target variable is discrete (e.g., True/False, spam/not spam).

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](09_principal_component_analysis.md) | [Next](11_linear_regression_multiple_variables.md)
