# 01. Linear Regression - Complete Mathematics

Linear Regression is the foundational supervised learning algorithm for predicting continuous values. This document covers the complete mathematical derivation from first principles.

## Table of Contents
1. [Problem Statement](#1-problem-statement)
2. [The Hypothesis Function](#2-the-hypothesis-function)
3. [Cost Function (Mean Squared Error)](#3-cost-function-mean-squared-error)
4. [Optimization: Finding the Best Parameters](#4-optimization-finding-the-best-parameters)
5. [Gradient Descent Derivation](#5-gradient-descent-derivation)
6. [Normal Equation (Closed-Form Solution)](#6-normal-equation-closed-form-solution)
7. [Worked Example](#7-worked-example)
8. [Evaluation Metrics for Regression](#8-evaluation-metrics-for-regression)

---

## 1. Problem Statement

**Goal**: Given a dataset of $m$ training examples $\{(x^{(1)}, y^{(1)}), (x^{(2)}, y^{(2)}), \dots, (x^{(m)}, y^{(m)})\}$, find the best-fitting straight line that predicts $y$ from $x$.

**Input**: Feature $x$ (e.g., house size in sq ft)

**Output**: Target $y$ (e.g., house price)

---

## 2. The Hypothesis Function

The hypothesis $h_\theta(x)$ is our prediction function. For simple linear regression (one feature):

$$h_\theta(x) = \theta_0 + \theta_1 x$$

Where:
- $\theta_0$: **Bias** (y-intercept) - the value of $y$ when $x = 0$
- $\theta_1$: **Weight** (slope) - how much $y$ changes for a unit change in $x$

**Matrix Form** (for scalability):
$$h_\theta(x) = \theta^T x$$

Where $\theta = \begin{bmatrix} \theta_0 \\ \theta_1 \end{bmatrix}$ and $x = \begin{bmatrix} 1 \\ x \end{bmatrix}$ (we add a 1 for the bias term).

---

## 3. Cost Function (Mean Squared Error)

We need a way to measure how "wrong" our predictions are. The **Cost Function** $J(\theta)$ quantifies the error.

$$J(\theta_0, \theta_1) = \frac{1}{2m} \sum_{i=1}^{m} \left( h_\theta(x^{(i)}) - y^{(i)} \right)^2$$

**Breakdown**:
1. $(h_\theta(x^{(i)}) - y^{(i)})$: Error for a single training example (prediction - actual)
2. $(...)^2$: Square the error to make all errors positive and penalize large errors more
3. $\sum$: Sum errors over all $m$ training examples
4. $\frac{1}{2m}$: Average the error ($\frac{1}{m}$). The $\frac{1}{2}$ is a convenience factor that simplifies the derivative later.

**Objective**: Minimize $J(\theta)$ to find the best $\theta_0$ and $\theta_1$.

---

## 4. Optimization: Finding the Best Parameters

There are two main methods to find the $\theta$ values that minimize $J(\theta)$:

| Method | Description | When to Use |
|---|---|---|
| **Gradient Descent** | Iterative algorithm that takes steps in the direction of the steepest descent | Large datasets, many features |
| **Normal Equation** | Closed-form (direct) solution using linear algebra | Small-medium datasets |

---

## 5. Gradient Descent Derivation

Gradient Descent repeatedly updates $\theta$ using:

$$\theta_j := \theta_j - \alpha \frac{\partial}{\partial \theta_j} J(\theta)$$

Where $\alpha$ is the **learning rate**.

### Deriving the Partial Derivatives

**Step 1**: Start with the cost function.
$$J(\theta) = \frac{1}{2m} \sum_{i=1}^{m} \left( h_\theta(x^{(i)}) - y^{(i)} \right)^2$$

**Step 2**: Apply the chain rule to find $\frac{\partial J}{\partial \theta_j}$.

Let $e^{(i)} = h_\theta(x^{(i)}) - y^{(i)}$ (the error for sample $i$).

$$\frac{\partial J}{\partial \theta_j} = \frac{1}{m} \sum_{i=1}^{m} e^{(i)} \cdot \frac{\partial}{\partial \theta_j} \left( h_\theta(x^{(i)}) \right)$$

Since $h_\theta(x) = \theta_0 \cdot 1 + \theta_1 \cdot x$:
- $\frac{\partial h_\theta}{\partial \theta_0} = 1$
- $\frac{\partial h_\theta}{\partial \theta_1} = x$

**Step 3**: Substitute back.

For $\theta_0$:
$$\frac{\partial J}{\partial \theta_0} = \frac{1}{m} \sum_{i=1}^{m} \left( h_\theta(x^{(i)}) - y^{(i)} \right)$$

For $\theta_1$:
$$\frac{\partial J}{\partial \theta_1} = \frac{1}{m} \sum_{i=1}^{m} \left( h_\theta(x^{(i)}) - y^{(i)} \right) \cdot x^{(i)}$$

### The Update Rules

**Repeat until convergence:**
$$\theta_0 := \theta_0 - \alpha \frac{1}{m} \sum_{i=1}^{m} \left( h_\theta(x^{(i)}) - y^{(i)} \right)$$
$$\theta_1 := \theta_1 - \alpha \frac{1}{m} \sum_{i=1}^{m} \left( h_\theta(x^{(i)}) - y^{(i)} \right) \cdot x^{(i)}$$

---

## 6. Normal Equation (Closed-Form Solution)

For small to medium datasets, we can skip iteration and compute $\theta$ directly.

### Matrix Formulation

Let:
- $X$ = Design Matrix (size $m \times (n+1)$), where each row is a training example.
  - We add a column of 1s for the bias term $\theta_0$.
- $y$ = Target vector (size $m \times 1$).
- $\theta$ = Parameter vector (size $(n+1) \times 1$).

$$X = \begin{bmatrix} 1 & x^{(1)} \\ 1 & x^{(2)} \\ \vdots & \vdots \\ 1 & x^{(m)} \end{bmatrix}, \quad y = \begin{bmatrix} y^{(1)} \\ y^{(2)} \\ \vdots \\ y^{(m)} \end{bmatrix}$$

### The Formula

$$\theta = (X^T X)^{-1} X^T y$$

**Derivation Sketch**:
1. Cost in matrix form: $J(\theta) = \frac{1}{2m}(X\theta - y)^T(X\theta - y)$
2. Take gradient w.r.t $\theta$ and set to zero.
3. Solve for $\theta$.

### Comparison

| Feature | Gradient Descent | Normal Equation |
|---|---|---|
| Learning Rate $\alpha$ | Need to choose | Not needed |
| Iterations | Many | None (one computation) |
| Complexity | $O(kn^2)$ | $O(n^3)$ for matrix inversion |
| Large $n$ (10,000+ features) | Works well | Very slow |

---

## 7. Worked Example

**Data**:

| $x$ (Size sq ft) | $y$ (Price $1000s) |
|---|---|
| 1 | 1 |
| 2 | 2 |
| 3 | 3 |

**Using Normal Equation**:

**Step 1**: Construct $X$ and $y$.
$$X = \begin{bmatrix} 1 & 1 \\ 1 & 2 \\ 1 & 3 \end{bmatrix}, \quad y = \begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix}$$

**Step 2**: Compute $X^T X$.
$$X^T X = \begin{bmatrix} 1 & 1 & 1 \\ 1 & 2 & 3 \end{bmatrix} \begin{bmatrix} 1 & 1 \\ 1 & 2 \\ 1 & 3 \end{bmatrix} = \begin{bmatrix} 3 & 6 \\ 6 & 14 \end{bmatrix}$$

**Step 3**: Compute $(X^T X)^{-1}$.
Determinant: $(3)(14) - (6)(6) = 42 - 36 = 6$.
$$(X^T X)^{-1} = \frac{1}{6} \begin{bmatrix} 14 & -6 \\ -6 & 3 \end{bmatrix} = \begin{bmatrix} 7/3 & -1 \\ -1 & 1/2 \end{bmatrix}$$

**Step 4**: Compute $X^T y$.
$$X^T y = \begin{bmatrix} 1 & 1 & 1 \\ 1 & 2 & 3 \end{bmatrix} \begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix} = \begin{bmatrix} 6 \\ 14 \end{bmatrix}$$

**Step 5**: Compute $\theta = (X^T X)^{-1} X^T y$.
$$\theta = \begin{bmatrix} 7/3 & -1 \\ -1 & 1/2 \end{bmatrix} \begin{bmatrix} 6 \\ 14 \end{bmatrix} = \begin{bmatrix} (7/3)(6) + (-1)(14) \\ (-1)(6) + (1/2)(14) \end{bmatrix} = \begin{bmatrix} 14 - 14 \\ -6 + 7 \end{bmatrix} = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$$

**Answer**: $\theta_0 = 0$, $\theta_1 = 1$.

**Model**: $h(x) = 0 + 1 \cdot x = x$ (The line passes perfectly through all points).

---

## 8. Evaluation Metrics for Regression

After training a regression model, we need to measure how well it performs.

### 8.1 Residuals

**Definition**: The difference between the actual value and the predicted value for each data point.

$$\text{Residual}_i = y^{(i)} - \hat{y}^{(i)}$$

Where $\hat{y}^{(i)} = h_\theta(x^{(i)})$ is the prediction.

**Interpretation**: Residuals should ideally be randomly scattered around zero. If there's a pattern, the model is missing something.

### 8.2 Sum of Squared Residuals (SS_res)

**Formula**:
$$SS_{res} = \sum_{i=1}^{m} (y^{(i)} - \hat{y}^{(i)})^2$$

**Interpretation**: Total squared error of the model's predictions. This is what we minimize during training.

### 8.3 Total Sum of Squares (SS_tot)

**Formula**:
$$SS_{tot} = \sum_{i=1}^{m} (y^{(i)} - \bar{y})^2$$

Where $\bar{y} = \frac{1}{m}\sum y^{(i)}$ is the mean of actual values.

**Interpretation**: Total variance in the data. How much the actual values deviate from their mean.

### 8.4 Mean Squared Error (MSE)

**Formula**:
$$MSE = \frac{1}{m} \sum_{i=1}^{m} (y^{(i)} - \hat{y}^{(i)})^2 = \frac{SS_{res}}{m}$$

**Interpretation**: Average of squared errors. Units are squared (e.g., $\text{dollars}^2$).

### 8.5 Root Mean Squared Error (RMSE)

**Formula**:
$$RMSE = \sqrt{MSE} = \sqrt{\frac{1}{m} \sum_{i=1}^{m} (y^{(i)} - \hat{y}^{(i)})^2}$$

**Interpretation**: Same units as the target variable. More interpretable than MSE. "On average, predictions are off by RMSE units."

### 8.6 Mean Absolute Error (MAE)

**Formula**:
$$MAE = \frac{1}{m} \sum_{i=1}^{m} |y^{(i)} - \hat{y}^{(i)}|$$

**Interpretation**: Average absolute error. Less sensitive to outliers than MSE/RMSE.

### 8.7 Coefficient of Determination (R²)

**Formula**:
$$R^2 = 1 - \frac{SS_{res}}{SS_{tot}}$$

**Interpretation**:
- $R^2 = 1$: Perfect fit (model explains 100% of variance)
- $R^2 = 0$: Model is as good as predicting the mean
- $R^2 < 0$: Model is worse than the mean (very bad!)

**Example**: $R^2 = 0.85$ means the model explains 85% of the variance in the target.

### 8.8 The Optimization Objective (argmin)

The goal of training is to find the parameters $\theta$ that minimize the cost:

$$\theta^* = \arg\min_{\theta} J(\theta)$$

Read as: "$\theta^*$ is the value of $\theta$ that minimizes $J(\theta)$."

Alternatively:
$$w^* = \arg\min_{w} J(w)$$

**Note**: $w$ (weights) and $\theta$ (parameters) are used interchangeably in ML literature.

### Summary Table

| Metric | Formula | Interpretation |
|---|---|---|
| **Residual** | $y - \hat{y}$ | Error for one point |
| **SS_res** | $\sum(y - \hat{y})^2$ | Total squared error |
| **SS_tot** | $\sum(y - \bar{y})^2$ | Total variance |
| **MSE** | $\frac{1}{m} \sum(y - \hat{y})^2$ | Avg squared error |
| **RMSE** | $\sqrt{MSE}$ | Avg error (same units) |
| **MAE** | $\frac{1}{m} \sum|y - \hat{y}|$ | Avg absolute error |
| **R²** | $1 - \frac{SS_{res}}{SS_{tot}}$ | % variance explained |

### Example Calculation

**Data**: Actual $y = [3, 5, 7]$, Predicted $\hat{y} = [2.5, 5.5, 6.5]$

1. **Residuals**: $[0.5, -0.5, 0.5]$
2. **SS_res**: $0.5^2 + 0.5^2 + 0.5^2 = 0.75$
3. **Mean** $\bar{y} = 5$
4. **SS_tot**: $(3-5)^2 + (5-5)^2 + (7-5)^2 = 4 + 0 + 4 = 8$
5. **MSE**: $0.75 / 3 = 0.25$
6. **RMSE**: $\sqrt{0.25} = 0.5$
7. **MAE**: $(0.5 + 0.5 + 0.5) / 3 = 0.5$
8. **R²**: $1 - (0.75 / 8) = 1 - 0.09375 = 0.906$ (90.6% variance explained)

---

**Next Topic:** [02. Polynomial Regression →](02_Polynomial_Regression.md)
