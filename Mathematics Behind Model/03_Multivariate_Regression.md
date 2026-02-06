# 03. Multivariate Regression - Complete Mathematics

Multivariate (Multiple) Regression extends Linear Regression to handle multiple input features. Instead of predicting house price from just size, we use size, bedrooms, age, location, etc.

## Table of Contents
1. [Problem Statement](#1-problem-statement)
2. [The Hypothesis Function](#2-the-hypothesis-function)
3. [Cost Function (Vector Form)](#3-cost-function-vector-form)
4. [Gradient Descent for Multiple Features](#4-gradient-descent-for-multiple-features)
5. [Feature Scaling & Normalization](#5-feature-scaling--normalization)
6. [Normal Equation](#6-normal-equation)
7. [Worked Example](#7-worked-example)

---

## 1. Problem Statement

**Given**: A dataset with $m$ training examples, each with $n$ features.

| Example | $x_1$ (Size) | $x_2$ (Bedrooms) | $x_3$ (Age) | $y$ (Price) |
|---|---|---|---|---|
| 1 | 2104 | 3 | 45 | 460 |
| 2 | 1416 | 2 | 40 | 232 |
| ... | ... | ... | ... | ... |

**Goal**: Find the relationship $y = f(x_1, x_2, \dots, x_n)$.

---

## 2. The Hypothesis Function

For $n$ features:

$$h_\theta(x) = \theta_0 + \theta_1 x_1 + \theta_2 x_2 + \dots + \theta_n x_n$$

### Compact Vector Notation

Let:
- $x = \begin{bmatrix} x_0 \\ x_1 \\ x_2 \\ \vdots \\ x_n \end{bmatrix}$ where $x_0 = 1$ (for $\theta_0$)
- $\theta = \begin{bmatrix} \theta_0 \\ \theta_1 \\ \theta_2 \\ \vdots \\ \theta_n \end{bmatrix}$

Then:
$$h_\theta(x) = \theta^T x = \sum_{j=0}^{n} \theta_j x_j$$

---

## 3. Cost Function (Vector Form)

**Scalar Form** (summing over all examples):
$$J(\theta) = \frac{1}{2m} \sum_{i=1}^{m} \left( h_\theta(x^{(i)}) - y^{(i)} \right)^2$$

**Matrix Form** (more efficient for computation):
$$J(\theta) = \frac{1}{2m} (X\theta - y)^T (X\theta - y)$$

Where:
- $X$ is the $m \times (n+1)$ design matrix (each row is a training example with $x_0 = 1$)
- $y$ is the $m \times 1$ target vector
- $\theta$ is the $(n+1) \times 1$ parameter vector

---

## 4. Gradient Descent for Multiple Features

The update rule extends naturally to all parameters:

**Repeat until convergence:**
$$\theta_j := \theta_j - \alpha \frac{\partial}{\partial \theta_j} J(\theta) \quad \text{(for all } j = 0, 1, \dots, n \text{)}$$

### The Partial Derivative

$$\frac{\partial J}{\partial \theta_j} = \frac{1}{m} \sum_{i=1}^{m} \left( h_\theta(x^{(i)}) - y^{(i)} \right) x_j^{(i)}$$

### Vectorized Update (Efficient)

$$\theta := \theta - \frac{\alpha}{m} X^T (X\theta - y)$$

This single matrix operation updates all parameters simultaneously.

---

## 5. Feature Scaling & Normalization

When features have different scales (e.g., Size: 1000-5000, Bedrooms: 1-5), Gradient Descent can oscillate and converge slowly.

**Types of Scaling**:

| Method | Formula | Range |
|---|---|---|
| **Min-Max** | $\frac{x - x_{min}}{x_{max} - x_{min}}$ | 0 to 1 |
| **Z-Score (Standardization)** | $\frac{x - \mu}{\sigma}$ | Approx -3 to 3 |
| **Mean Normalization** | $\frac{x - \mu}{x_{max} - x_{min}}$ | Approx -0.5 to 0.5 |

**Goal**: Get all features into approximately the same range (e.g., $-1 \le x \le 1$).

---

## 6. Normal Equation

The closed-form solution works for any number of features:

$$\theta = (X^T X)^{-1} X^T y$$

### Advantages
- No learning rate to choose
- No iterations

### Disadvantages
- Computing $(X^T X)^{-1}$ is $O(n^3)$
- If $X^T X$ is singular (non-invertible):
  - Redundant features (linearly dependent)
  - Too many features ($n > m$)
  - Solution: Use pseudo-inverse or regularization

---

## 7. Worked Example

**Data** (predicting price from size and bedrooms):

| Size ($x_1$) | Bedrooms ($x_2$) | Price ($y$) |
|---|---|---|
| 1 | 1 | 1 |
| 2 | 2 | 4 |
| 3 | 3 | 7 |

**Using Normal Equation**:

**Step 1**: Construct $X$ and $y$.
$$X = \begin{bmatrix} 1 & 1 & 1 \\ 1 & 2 & 2 \\ 1 & 3 & 3 \end{bmatrix}, \quad y = \begin{bmatrix} 1 \\ 4 \\ 7 \end{bmatrix}$$

**Step 2**: Compute $X^T X$.
$$X^T X = \begin{bmatrix} 3 & 6 & 6 \\ 6 & 14 & 14 \\ 6 & 14 & 14 \end{bmatrix}$$

**Note**: This matrix is **singular** (columns 2 and 3 are identical because $x_1 = x_2$). We have **multicollinearity**.

**Solution**: Remove redundant feature or use regularization.

**If using only $x_1$**:
$$X = \begin{bmatrix} 1 & 1 \\ 1 & 2 \\ 1 & 3 \end{bmatrix}$$

Following the same steps as Linear Regression:

**Answer**: $\theta_0 = -2$, $\theta_1 = 3$.

**Model**: $h(x) = -2 + 3x_1$

**Check**: $h(1) = 1$, $h(2) = 4$, $h(3) = 7$ ✓

---

**Previous Topic:** [← 02. Polynomial Regression](02_Polynomial_Regression.md) | **Next Topic:** [04. Logistic Regression →](04_Logistic_Regression.md)
