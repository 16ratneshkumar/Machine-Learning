# 17. Logistic Regression

## 1. Overview
Logistic Regression is a classification algorithm used to model the probability of a discrete response (typically binary) based on one or more predictor variables. Despite its name, it is fundamentally a classification technique, not regression.

## 2. Core Concepts
- **Limitation of Linear Models:** A standard linear model ($p(X) = \beta_0 + \beta_1 X$) can produce invalid probabilities less than 0 or greater than 1.
- **The Logistic Function:** To map outputs strictly between 0 and 1, the model uses the logistic (sigmoid) function.
  *Example (Default Dataset):* Modeling the probability of a credit card default based on the user's `balance`: $Pr(\text{default} = \text{Yes} | \text{balance})$. The logistic function ensures $p(\text{balance})$ will always range strictly between 0 and 1.
  $$ p(X) = \frac{e^{\beta_0 + \beta_1 X}}{1 + e^{\beta_0 + \beta_1 X}} $$

## 3. Mathematical Formulation
By algebraically manipulating the logistic function, we define the **Odds** and the **Logit**:

**Odds:** The ratio of the probability of success to the probability of failure:
$$ \frac{p(X)}{1-p(X)} = e^{\beta_0 + \beta_1 X} $$

**Log-Odds (Logit):** Taking the logarithm of the odds yields a linear relationship with the predictors:
$$ \log\left(\frac{p(X)}{1-p(X)}\right) = \beta_0 + \beta_1 X $$
*For multiple predictors, the logit extends naturally: $\beta_0 + \beta_1 X_1 + \dots + \beta_p X_p$*

## 4. Estimation & Inference
- **Maximum Likelihood Estimation (MLE):** Unlike linear regression which uses Ordinary Least Squares, logistic regression parameters are estimated by maximizing the likelihood function.
- **Coefficient Interpretation:** A positive coefficient ($\beta_j > 0$) means that an increase in $X_j$ increases the log-odds, thereby increasing the probability of the positive class.
- **Significance:** Evaluated using z-statistics and corresponding p-values.
- **Qualitative Predictors:** Categorical variables are handled with dummy variables (e.g., student vs. non-student status).
- **Source caution (confounding effect):** A coefficient sign for a dummy variable can reverse when adding other predictors (for example, positive in a one-variable model but negative after adjusting for `balance`), so interpretation must be conditional on the full model.

## 5. Classification Mechanics
After computing the predicted probability $\hat{p}(X)$, a threshold $\theta$ is applied to convert the continuous probability into a discrete class label.
- **Default Threshold:** Usually $0.5$ ($\hat{p} > 0.5 \implies \text{Class 1}$).
- **Risk-Adjusted Threshold:** Can be shifted (e.g., to $0.1$ or $0.9$) to minimize false negatives or false positives depending on domain-specific costs (e.g., medical diagnoses).
- Logistic regression scores are often compared to LDA/SVM on ROC curves; in source examples, logistic-style boundary methods are less sensitive to points far from the decision boundary than methods that depend on full class covariance estimation.

## 6. Logistic Curve

```text
    P(Y=1)
     1.0 |                   .-------
         |                 .
         |               .
     0.5 |-------------+-------------  <-- Decision Threshold
         |           .
         |         .
     0.0 +-------.-------------------
         ----------------------------> Logit (β_0 + β_1 X)
```

## Use Cases & Limitations

**5 Use Cases (When to use):**
1. **Binary Classification:** The go-to baseline model for predicting binary outcomes (e.g., Spam vs. Not Spam, Fraud vs. Legitimate).
2. **Medical Diagnosis:** Widely used in healthcare to model the probability of a patient having a specific disease based on diagnostic metrics (due to its high interpretability).
3. **Credit Scoring:** Used by financial institutions to calculate the probability of a customer defaulting on a loan based on their financial history.
4. **Customer Churn Prediction:** Predicting whether a subscriber will cancel their service, allowing businesses to target retention efforts.
5. **Marketing Conversion:** Estimating the likelihood that a user will click an ad or make a purchase based on demographic and behavioral data.

**5 Limitations (When NOT to use):**
1. **Non-Linear Boundaries:** Assumes a linear decision boundary between classes. It cannot solve problems where the classes are separated by complex, non-linear shapes without heavy feature engineering.
2. **Multicollinearity:** Highly sensitive to correlated independent variables, which can severely distort the learned coefficients and their statistical significance.
3. **Feature Scaling Sensitivity:** Requires features to be normalized/standardized for the gradient descent optimization to converge efficiently and for regularization to work properly.
4. **Overfitting with Sparse Data:** Prone to severe overfitting if the number of features exceeds the number of observations, requiring strict regularization (L1/L2).
5. **Target Class Imbalance:** Struggles with heavily imbalanced datasets, often predicting the majority class universally unless weights or thresholds are explicitly adjusted.

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](16_naive_bayes_classifier.md) | [Next](18_k_nearest_neighbor.md)
