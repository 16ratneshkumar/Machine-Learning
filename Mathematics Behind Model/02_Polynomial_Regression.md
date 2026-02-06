# 02. Polynomial Regression - Complete Mathematics

Polynomial Regression extends Linear Regression to model non-linear relationships by adding polynomial terms of the original features.

## Table of Contents
1. [Motivation](#1-motivation)
2. [The Polynomial Hypothesis](#2-the-polynomial-hypothesis)
3. [Feature Engineering](#3-feature-engineering)
4. [Cost Function & Optimization](#4-cost-function--optimization)
5. [Overfitting and Underfitting](#5-overfitting-and-underfitting)
6. [Worked Example](#6-worked-example)

---

## 1. Motivation

Linear Regression fits a straight line. But what if the data follows a curve?

**Example**: Predicting crop yield vs. temperature. Too cold or too hot is bad; there's an optimal range. A straight line can't capture this "U-shape" or "inverted U-shape".

**Solution**: Use polynomial features like $x^2$, $x^3$, etc., to allow the model to learn curves.

---

## 2. The Polynomial Hypothesis

For a degree-$d$ polynomial:

$$h_\theta(x) = \theta_0 + \theta_1 x + \theta_2 x^2 + \theta_3 x^3 + \dots + \theta_d x^d$$

This is still **linear in the parameters** $\theta$, even though it's non-linear in the input $x$. This is the key insight that allows us to use the same optimization techniques.

### Examples by Degree

| Degree | Equation | Shape |
|---|---|---|
| 1 | $\theta_0 + \theta_1 x$ | Straight Line |
| 2 | $\theta_0 + \theta_1 x + \theta_2 x^2$ | Parabola (U or ∩) |
| 3 | $\theta_0 + \theta_1 x + \theta_2 x^2 + \theta_3 x^3$ | S-curve possible |

---

## 3. Feature Engineering

Polynomial Regression is achieved by transforming the original feature $x$ into multiple features.

**Original Data**: $x$
**Transformed Features**: $[1, x, x^2, x^3, \dots, x^d]$

We create a new "design matrix" with these transformed features and then apply standard Linear Regression.

### Matrix Formulation

For $m$ training examples and degree $d$:

$$X = \begin{bmatrix} 1 & x^{(1)} & (x^{(1)})^2 & \dots & (x^{(1)})^d \\ 1 & x^{(2)} & (x^{(2)})^2 & \dots & (x^{(2)})^d \\ \vdots & \vdots & \vdots & \ddots & \vdots \\ 1 & x^{(m)} & (x^{(m)})^2 & \dots & (x^{(m)})^d \end{bmatrix}$$

### Feature Scaling (Important!)

When using polynomial features, the values can become very large (e.g., if $x = 1000$, then $x^2 = 1,000,000$). This causes issues for Gradient Descent.

**Solution**: Normalize features to a similar scale (e.g., 0 to 1 or -1 to 1).

**Formula (Min-Max Scaling)**:
$$x_{scaled} = \frac{x - x_{min}}{x_{max} - x_{min}}$$

---

## 4. Cost Function & Optimization

Once features are transformed, the cost function and optimization are **identical to Linear Regression**.

**Cost Function**:
$$J(\theta) = \frac{1}{2m} \sum_{i=1}^{m} \left( h_\theta(x^{(i)}) - y^{(i)} \right)^2$$

Where $h_\theta(x^{(i)})$ uses the polynomial features.

**Normal Equation** (still works):
$$\theta = (X^T X)^{-1} X^T y$$

Where $X$ is the transformed design matrix with polynomial columns.

---

## 5. Overfitting and Underfitting

Choosing the polynomial degree $d$ is critical.

| Scenario | Description | Problem |
|---|---|---|
| **Underfitting** (High Bias) | Degree too low (e.g., $d=1$ for curved data) | Model is too simple, misses the pattern |
| **Overfitting** (High Variance) | Degree too high (e.g., $d=10$ for 5 data points) | Model memorizes training data, fails on new data |

### The Bias-Variance Tradeoff

- **Low Degree**: High Bias, Low Variance
- **High Degree**: Low Bias, High Variance

**Solution**: Use **Regularization** (Ridge, Lasso) or **Cross-Validation** to find the optimal degree.

---

## 6. Worked Example

**Data**:

| $x$ | $y$ |
|---|---|
| 1 | 1 |
| 2 | 4 |
| 3 | 9 |

**Observation**: $y = x^2$ (a quadratic relationship).

**Using Degree-2 Polynomial ($d=2$)**:

**Step 1**: Transform features.
$$X = \begin{bmatrix} 1 & 1 & 1 \\ 1 & 2 & 4 \\ 1 & 3 & 9 \end{bmatrix}, \quad y = \begin{bmatrix} 1 \\ 4 \\ 9 \end{bmatrix}$$

**Step 2**: Apply Normal Equation $\theta = (X^T X)^{-1} X^T y$.

(After matrix calculations...)

**Answer**: $\theta_0 = 0$, $\theta_1 = 0$, $\theta_2 = 1$.

**Model**: $h(x) = 0 + 0 \cdot x + 1 \cdot x^2 = x^2$ (Perfect fit!)

---

**Previous Topic:** [← 01. Linear Regression](01_Linear_Regression.md) | **Next Topic:** [03. Multivariate Regression →](03_Multivariate_Regression.md)
