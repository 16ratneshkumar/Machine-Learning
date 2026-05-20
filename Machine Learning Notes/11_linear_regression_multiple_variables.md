# 11. Multiple Linear Regression

## 1. Overview
Multiple Linear Regression extends simple linear regression to model the relationship between a continuous quantitative response variable and two or more predictor variables.

## 2. The Linear Model
**Theoretical Stochastic Form:**
$$ Y = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \dots + \beta_p X_p + \epsilon $$

**Interpretation of Coefficients:**
- $\beta_0$: Intercept (expected response when all predictors $X_j = 0$).
- $\beta_j$: The average change in the response $Y$ for a one-unit increase in predictor $X_j$, **holding all other predictors fixed**.

**Prediction Model:**
$$ \hat{y} = \hat{\beta}_0 + \hat{\beta}_1 x_1 + \dots + \hat{\beta}_p x_p $$

## 3. Ordinary Least Squares (OLS) Estimation
The objective remains to minimize the **Residual Sum of Squares (RSS)**:
$$ \text{RSS} = \sum_{i=1}^{n} (y_i - \hat{y}_i)^2 $$

In matrix notation, the closed-form solution for the coefficient vector $\hat{\beta}$ is:
$$ \hat{\beta} = (X^T X)^{-1} X^T y $$
*(Where $X$ is the design matrix and $y$ is the vector of responses).*

## 4. Statistical Inference & Evaluation
### Hypothesis Testing (Global Significance)
To determine if *any* predictor is useful:
- **Null Hypothesis ($H_0$):** $\beta_1 = \beta_2 = \dots = \beta_p = 0$
- **F-statistic:**
  $$ F = \frac{(\text{TSS} - \text{RSS})/p}{\text{RSS}/(n-p-1)} $$
  > A large F-statistic with a tiny p-value indicates that at least one predictor contributes significantly to the model.
- **Expectation under $H_0$:** If there is no relationship, $E[\text{RSS}/(n-p-1)] = \sigma^2$ and $E[(\text{TSS}-\text{RSS})/p] = \sigma^2$, so we expect $F \approx 1$. If $H_a$ is true, $F$ will be significantly greater than 1 (e.g., an F-statistic of 570 in an advertising model provides compelling evidence to reject $H_0$).

### Partial F-Test (Nested Models)
To test whether a specific subset of predictors adds value, compare:
- **Reduced model:** excludes the subset
- **Full model:** includes the subset

If $q$ predictors are added, with $\text{RSS}_0$ (reduced) and $\text{RSS}$ (full):
$$ F = \frac{(\text{RSS}_0 - \text{RSS})/q}{\text{RSS}/(n-p-1)} $$
This isolates the incremental explanatory power of the added predictors.

### Confusing Correlated Predictors
- Performing separate simple regressions can be heavily misleading if predictors are correlated (confounding variables/surrogates).
- *Example (Advertising):* Newspaper advertising may appear highly effective on its own, but its effect vanishes when controlling for TV and Radio advertising, because newspaper is just correlated with radio.
- *Example (Absurd):* A simple regression might show a positive relationship between ice cream sales and shark attacks. However, a multiple regression adjusting for *temperature* will reveal that ice cream sales are not actually a significant predictor of shark attacks; they are merely a surrogate for warm weather.

### Synergy & Interaction Effects
- Multiple regression assumes the effect of one predictor is independent of others (additivity). However, predictors often interact.
- **Synergy:** In marketing, spending \$50,000 on TV and \$50,000 on Radio simultaneously might generate higher sales than spending \$100,000 on either individually. In statistics, this is modeled by an **interaction effect** term (e.g., $\beta_3 X_1 X_2$).

## 5. Matrix Transformation Flow

```text
  [Design Matrix X (n x p)]     [Response Vector Y (n x 1)]
               \                     /
                v                   v
             [ Ordinary Least Squares ]
               (X^T X)^-1 X^T Y
                        |
                        v
        [Coefficient Vector β_hat (p x 1)]
```

## Use Cases & Limitations

**5 Use Cases (When to use):**
1. **Real Estate Pricing:** Predicting house prices based on multiple features like square footage, number of bedrooms, and neighborhood.
2. **Marketing Mix Modeling:** Determining the combined effect of different advertising channels (TV, Radio, Social Media) on overall sales.
3. **Medical Research:** Analyzing the impact of multiple physiological factors (BMI, age, blood pressure) on disease progression metrics.
4. **Financial Forecasting:** Predicting economic indicators like inflation rates based on interest rates, unemployment, and GDP growth.
5. **Performance Evaluation:** Estimating an employee's performance score based on years of experience, education level, and training hours.

**5 Limitations (When NOT to use):**
1. **Multicollinearity:** Fails or becomes highly unstable when independent variables are highly correlated with each other (e.g., using both "years of age" and "months of age").
2. **Assumption Violations:** Heavily relies on strict statistical assumptions (linearity, independence, homoscedasticity, normality of errors).
3. **Extrapolation Danger:** Dangerous when making predictions outside the range of the observed training data, leading to absurd results.
4. **Overfitting with Many Features:** Including too many irrelevant predictors can cause the model to overfit the training data, reducing generalization.
5. **Complex Interactions:** While interaction terms can be added, it struggles to automatically capture deep, complex, non-linear interactions without manual feature engineering.

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](10_linear_regression_single_variable.md) | [Next](12_gradient_descent.md)
