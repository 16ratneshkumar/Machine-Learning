# 02. Statistics & Probability for Machine Learning

Statistics provides the tools to analyze and interpret data, while Probability allows us to reason about uncertainty and make predictions.

## Table of Contents
1. [Mean (Expected Value)](#1-mean-expected-value)
2. [Variance & Standard Deviation](#2-variance--standard-deviation)
3. [Normalization (Z-Score)](#3-normalization-z-score)
4. [Conditional Probability](#4-conditional-probability)
5. [Bayes' Theorem](#5-bayes-theorem)
6. [Probability Distributions (Normal / Gaussian)](#6-probability-distributions-normal--gaussian)
7. [Covariance & Correlation](#7-covariance--correlation)

---

## 1. Mean (Expected Value)

The mean is the central value of a set of numbers. It is the most common measure of "central tendency," representing the balancing point of the data. In probability terms, the Expected Value is the theoretical mean of a random variable over infinite trials.

### Formula
$\mu = \frac{1}{n} \sum_{i=1}^{n} x_i$

### Application in Machine Learning
-   **Data Imputation**: When datasets have missing entries (NaNs), a common strategy is to fill them with the mean value of that column to preserve the general distribution.
-   **Baseline Prediction**: For regression tasks, a model that simply predicts the mean of the training target every time provides a "baseline" error. Any sophisticated ML model must beat this baseline to be considered useful.

### Example Problem

**Question**: Find the mean height of a group: $[150, 160, 170]$.

**Solution**:
1.  Sum: $150 + 160 + 170 = 480$.
2.  Count $n = 3$.
3.  Mean: $480 / 3 = 160$.


**Answer**: $160$

---

## 2. Variance & Standard Deviation

These metrics quantify the "spread" or "dispersion" of data.
-   **Variance**: The average of the squared differences from the mean. It gives a sense of how widely the data points deviate.
-   **Standard Deviation**: The square root of the variance. It is preferred for reporting because it is in the same units as the original data (e.g., "cms" instead of "cms squared").

### Formulas
-   **Variance ($\sigma^2$)**: $\frac{1}{n} \sum (x_i - \mu)^2$
-   **Std Dev ($\sigma$)**: $\sqrt{\sigma^2}$

### Application in Machine Learning
-   **Feature Scaling**: Understanding the spread is crucial. If one feature has a variance of 0.1 and another has 10,000, the second will dominate distance calculations in algorithms like KNN or Gradient Descent.
-   **Bias-Variance Tradeoff**: We analyze validation error to see if a model has "High Variance" (overfitting to noise in training data) or "High Bias" (underfitting/too simple).

### Example Problem

**Question**: Heights $[1, 2, 3]$. Mean is 2. Find Variance.

**Solution**:
1.  Diffs from mean: $(1-2)=-1, (2-2)=0, (3-2)=1$.
2.  Squares: $(-1)^2=1, 0^2=0, 1^2=1$.
3.  Average of squares: $(1+0+1)/3 = 2/3 \approx 0.67$.


**Answer**: Variance $\approx 0.67$

---

## 3. Normalization (Z-Score)

Normalization (specifically Standardization) is the process of rescaling data so it follows a standard normal distribution. This transforms the data to have a mean of 0 and a standard deviation of 1. It helps in comparing different features on equal footing.

### Formula
$z = \frac{x - \mu}{\sigma}$

### Application in Machine Learning
-   **Gradient Descent Optimization**: When features are on different scales (e.g., "Age" vs "Salary"), the cost function becomes an elongated valley, making gradient descent oscillate and converge slowly. Normalization makes the cost function spherical, allowing direct and fast convergence.
-   **Distance-Based Algorithms**: In K-Means or KNN, large-scale features can unjustly influence the result. Normalization ensures all features contribute equally to the distance.

### Example Problem

**Question**: Score $x=80$, Class Mean $\mu=60$, StdDev $\sigma=10$.

**Solution**:
1.  Deviation: $80 - 60 = 20$.
2.  Scale: $20 / 10 = 2$.


**Answer**: $z=2$ (The score is 2 standard deviations above average).

---

## 4. Conditional Probability

This measures the probability of an event happening *given that* another event has already occurred. It allows us to update our predictions based on new information (constraints).

### Formula
$P(A|B) = \frac{P(A \cap B)}{P(B)}$ "Probability of A given B"

### Application in Machine Learning
-   **Nature using Context**: In NLP, we don't just ask "What is the probability of the word 'Bank'?". We ask "What is the probability of 'Bank' GIVEN the previous word was 'River'?". This conditional context drastically changes the meaning and prediction.
-   **Decision Trees**: Splits in a tree are essentially creating conditional probabilities. "What is the chance this passenger survived GIVEN Sex=Female?".

### Example Problem

**Question**: 100 emails. 40 are Spam. Of those 40 Spam, 20 contain "Buy". Total emails with "Buy" is 25. Find $P(\text{Spam} | \text{Buy})$.

**Solution**:
1.  $P(\text{Spam} \cap \text{Buy})$: 20 emails / 100 = 0.2.
2.  $P(\text{Buy})$: 25 emails / 100 = 0.25.
3.  Formula: $0.2 / 0.25 = 0.8$.


**Answer**: $80\%$ chance it is spam if it contains "Buy".

---

## 5. Bayes' Theorem

Bayes' theorem provides a principled way of calculating a conditional probability. It links $P(A|B)$ with $P(B|A)$. It allows us to reverse the condition: if we know how likely Evidence is given a Cause, we can figure out how likely the Cause is given the Evidence.

### Formula
$P(A|B) = \frac{P(B|A) \cdot P(A)}{P(B)}$
-   **Posterior** = (Likelihood $\times$ Prior) / Evidence

### Application in Machine Learning
-   **Naive Bayes Classifier**: A probabilistic classifier based on applying this theorem. It assumes independence between features. It is incredibly fast and efficient for text classification (Spam detection, Sentiment Analysis) and serves as a strong baseline.
-   **Bayesian Neural Networks**: These estimate uncertainty in weights, allowing the model to say "I don't know" rather than confidently predicting wrong.

### Example Problem
**Question**:
-   $P(\text{Rain}) = 0.1$
-   $P(\text{Cloudy} | \text{Rain}) = 1.0$ (Always cloudy if raining)
-   $P(\text{Cloudy}) = 0.5$ (50% of days are cloudy)
    Find $P(\text{Rain} | \text{Cloudy})$.

**Solution**:
1.  Likelihood $\times$ Prior: $1.0 \times 0.1 = 0.1$.
2.  Divide by Evidence: $0.1 / 0.5 = 0.2$.


**Answer**: $20\%$ chance it is raining given it is cloudy.

---

## 6. Probability Distributions (Normal / Gaussian)

A probability distribution describes how the values of a random variable are distributed. The most important one in ML is the Normal (Gaussian) Distribution, distinguishable by its bell-shaped curve.

### Formula
$f(x) = \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{1}{2}(\frac{x-\mu}{\sigma})^2}$

### Application in Machine Learning
-   **Assumption of Normality**: Many algorithms (Linear Regression, Naive Bayes, Linear Discriminant Analysis) assume that the data follows a normal distribution. If the data is skewed, we often transform it (using Log transform) to make it look "Normal" so these algorithms work better.
-   **Central Limit Theorem**: States that the sum of many independent variables tends to look like a normal distribution, regardless of the original distribution.

### Example Problem

**Question**: In a standard normal distribution ($\mu=0, \sigma=1$), roughly what percentage of data falls within $\pm 1$ standard deviation?

**Solution**:
1.  This is a property of the Empirical Rule (68-95-99.7).
2.  Range $[-1, 1]$ covers the central peak.

**Answer**: $\approx 68\%$

---

## 7. Covariance & Correlation

These measure the relationship between two variables.
-   **Covariance**: Measures distinct *direction* of the relationship (positive = they grow together, negative = they move opposite).
-   **Correlation (Pearson)**: A normalized version of covariance between -1 and 1. It measures the *strength* and *direction*.

### Formulas
-   **Covariance**: $Cov(X, Y) = \frac{1}{n} \sum (x_i - \mu_x)(y_i - \mu_y)$
-   **Correlation**: $\rho = \frac{Cov(X, Y)}{\sigma_x \sigma_y}$

### Application in Machine Learning
-   **Feature Selection**: High correlation between two input features (Multicollinearity) is bad for linear models because they provide redundant information. We usually calculate a "Correlation Matrix" and drop one of the highly correlated features.

### Example Problem

**Question**: Data $X=[1, 2]$, $Y=[2, 4]$. Find Correlation.

**Solution**:
1.  Means: $\mu_x=1.5$, $\mu_y=3$.
2.  Covariance:
    -   $(1-1.5)(2-3) = (-0.5)(-1) = 0.5$
    -   $(2-1.5)(4-3) = (0.5)(1) = 0.5$
    -   Sum = 1.0, Avg = 0.5.
3.  Std Devs:
    -   $\sigma_x = \sqrt{((-0.5)^2 + 0.5^2)/2} = 0.5$
    -   $\sigma_y = \sqrt{((-1)^2 + 1^2)/2} = 1.0$
4.  Correlation: $0.5 / (0.5 \times 1.0) = 1$.

**Answer**: $1.0$ (Perfect positive correlation).

---

**Previous Topic:** [← 01. Linear Algebra](01_Linear_Algebra.md) | **Next Topic:** [03. Calculus →](03_Calculus.md)
