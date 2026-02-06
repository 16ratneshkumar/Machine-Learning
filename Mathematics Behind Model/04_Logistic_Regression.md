# 04. Logistic Regression - Complete Mathematics (Classification)

Logistic Regression is the foundational supervised learning algorithm for **binary classification** (Yes/No, Spam/Not Spam, 0/1). Despite its name, it is used for classification, not regression.

## Table of Contents
1. [Problem Statement](#1-problem-statement)
2. [Why Not Linear Regression?](#2-why-not-linear-regression)
3. [The Sigmoid (Logistic) Function](#3-the-sigmoid-logistic-function)
4. [The Hypothesis Function](#4-the-hypothesis-function)
5. [Decision Boundary](#5-decision-boundary)
6. [Cost Function (Log Loss / Binary Cross-Entropy)](#6-cost-function-log-loss--binary-cross-entropy)
7. [Gradient Descent Derivation](#7-gradient-descent-derivation)
8. [Worked Example](#8-worked-example)
9. [Evaluation Metrics](#9-evaluation-metrics)
10. [Multiclass Classification (One-vs-All)](#10-multiclass-classification-one-vs-all)

---

## 1. Problem Statement

**Goal**: Given a dataset of $m$ training examples $\{(x^{(1)}, y^{(1)}), \dots, (x^{(m)}, y^{(m)})\}$ where $y \in \{0, 1\}$, learn a model to predict the probability that a new input belongs to class 1.

**Examples**:
- Spam Detection: $x$ = email features, $y$ = 1 (spam) or 0 (not spam)
- Tumor Classification: $x$ = tumor size, $y$ = 1 (malignant) or 0 (benign)

---

## 2. Why Not Linear Regression?

Using $h_\theta(x) = \theta^T x$ for classification has problems:

1. **Output Range**: Linear regression outputs can be $< 0$ or $> 1$, but probabilities must be in $[0, 1]$.
2. **Sensitivity to Outliers**: A single extreme data point can drastically shift the decision boundary.

**Solution**: We need a function that "squashes" any input to the range $(0, 1)$.

---

## 3. The Sigmoid (Logistic) Function

The **sigmoid function** maps any real number to $(0, 1)$:

$$\sigma(z) = \frac{1}{1 + e^{-z}}$$

### Properties

| Input $z$ | Output $\sigma(z)$ |
|---|---|
| $z \to +\infty$ | $\sigma(z) \to 1$ |
| $z = 0$ | $\sigma(z) = 0.5$ |
| $z \to -\infty$ | $\sigma(z) \to 0$ |

### Graph Shape
An S-curve centered at $z = 0$.

### Key Derivative (Used in Gradient Descent)
$$\frac{d\sigma}{dz} = \sigma(z)(1 - \sigma(z))$$

---

## 4. The Hypothesis Function

We wrap the linear combination inside the sigmoid:

$$h_\theta(x) = \sigma(\theta^T x) = \frac{1}{1 + e^{-\theta^T x}}$$

**Interpretation**: $h_\theta(x)$ is the **probability** that $y = 1$ given input $x$.

$$h_\theta(x) = P(y = 1 | x; \theta)$$

Since probabilities sum to 1:
$$P(y = 0 | x; \theta) = 1 - h_\theta(x)$$

---

## 5. Decision Boundary

We classify based on a threshold (usually 0.5):

- If $h_\theta(x) \ge 0.5$, predict $y = 1$
- If $h_\theta(x) < 0.5$, predict $y = 0$

Since $\sigma(z) = 0.5$ when $z = 0$:
- Predict 1 if $\theta^T x \ge 0$
- Predict 0 if $\theta^T x < 0$

**The Decision Boundary** is the line (or hyperplane) where $\theta^T x = 0$.

### Example
If $\theta = [-3, 1, 1]^T$ and $x = [1, x_1, x_2]^T$:

$$-3 + x_1 + x_2 = 0 \implies x_1 + x_2 = 3$$

This is a straight line in 2D feature space.

---

## 6. Cost Function (Log Loss / Binary Cross-Entropy)

We **cannot use MSE** for Logistic Regression because when combined with sigmoid, the cost becomes non-convex (has many local minima).

### The Log Loss Function

For a single training example:
$$Cost(h_\theta(x), y) = \begin{cases} -\log(h_\theta(x)) & \text{if } y = 1 \\ -\log(1 - h_\theta(x)) & \text{if } y = 0 \end{cases}$$

**Intuition**:
- If $y = 1$ and $h_\theta(x) = 1$ (confident & correct): $-\log(1) = 0$ (no cost)
- If $y = 1$ and $h_\theta(x) = 0$ (confident & wrong): $-\log(0) = \infty$ (huge cost)

### Combined Formula

$$J(\theta) = -\frac{1}{m} \sum_{i=1}^{m} \left[ y^{(i)} \log(h_\theta(x^{(i)})) + (1 - y^{(i)}) \log(1 - h_\theta(x^{(i)})) \right]$$

This is **convex**, guaranteeing a global minimum.

---

## 7. Gradient Descent Derivation

**Update Rule** (same form as Linear Regression!):
$$\theta_j := \theta_j - \alpha \frac{\partial J}{\partial \theta_j}$$

### Deriving the Partial Derivative

**Step 1**: Start with the cost function for one example:
$$J = -[y \log(h) + (1-y) \log(1-h)]$$

**Step 2**: Use chain rule.
$$\frac{\partial J}{\partial \theta_j} = \frac{\partial J}{\partial h} \cdot \frac{\partial h}{\partial z} \cdot \frac{\partial z}{\partial \theta_j}$$

Where $z = \theta^T x$ and $h = \sigma(z)$.

**Step 3**: Compute each part.
- $\frac{\partial J}{\partial h} = -\frac{y}{h} + \frac{1-y}{1-h}$
- $\frac{\partial h}{\partial z} = h(1-h)$ (sigmoid derivative)
- $\frac{\partial z}{\partial \theta_j} = x_j$

**Step 4**: Combine and simplify (the algebra works out beautifully).
$$\frac{\partial J}{\partial \theta_j} = (h_\theta(x) - y) x_j$$

### The Update Rules

$$\theta_j := \theta_j - \frac{\alpha}{m} \sum_{i=1}^{m} \left( h_\theta(x^{(i)}) - y^{(i)} \right) x_j^{(i)}$$

**Note**: This looks identical to Linear Regression, but $h_\theta(x)$ is the sigmoid output.

### Vectorized Form
$$\theta := \theta - \frac{\alpha}{m} X^T (\sigma(X\theta) - y)$$

---

## 8. Worked Example

**Data** (Tumor classification):

| Size ($x$) | Malignant ($y$) |
|---|---|
| 1 | 0 |
| 2 | 0 |
| 3 | 1 |
| 4 | 1 |

**Iteration 1** (Initialize $\theta_0 = 0, \theta_1 = 0$, $\alpha = 0.1$):

**Step 1**: Compute predictions.
$z = \theta_0 + \theta_1 x = 0$ for all.
$h = \sigma(0) = 0.5$ for all.

**Step 2**: Compute errors $(h - y)$.
- $(0.5 - 0) = 0.5$ for $x = 1, 2$
- $(0.5 - 1) = -0.5$ for $x = 3, 4$

**Step 3**: Compute gradients.
$\frac{\partial J}{\partial \theta_0} = \frac{1}{4}(0.5 + 0.5 - 0.5 - 0.5) = 0$
$\frac{\partial J}{\partial \theta_1} = \frac{1}{4}(0.5(1) + 0.5(2) - 0.5(3) - 0.5(4)) = \frac{1}{4}(0.5 + 1 - 1.5 - 2) = -0.5$

**Step 4**: Update parameters.
$\theta_0 = 0 - 0.1(0) = 0$
$\theta_1 = 0 - 0.1(-0.5) = 0.05$

**After many iterations**: The model learns to separate classes 0 and 1 based on size.

---

## 9. Evaluation Metrics

After building a classifier, we need to measure its performance. These metrics are derived from the **Confusion Matrix**.

### 9.1 Confusion Matrix

|  | **Predicted: 1** | **Predicted: 0** |
|---|---|---|
| **Actual: 1** | True Positive (TP) | False Negative (FN) |
| **Actual: 0** | False Positive (FP) | True Negative (TN) |

- **TP**: Correctly predicted positive (e.g., correctly identified spam)
- **TN**: Correctly predicted negative (e.g., correctly identified not spam)
- **FP**: Incorrectly predicted positive (Type I Error - "False Alarm")
- **FN**: Incorrectly predicted negative (Type II Error - "Missed Detection")

### 9.2 Accuracy

**Formula**:
$$\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}$$

**Interpretation**: Out of all predictions, how many were correct?

**Limitation**: Misleading when classes are imbalanced. If 95% of emails are not spam, a model that always predicts "not spam" has 95% accuracy but is useless.

### 9.3 Precision

**Formula**:
$$\text{Precision} = \frac{TP}{TP + FP}$$

**Interpretation**: Of all the examples the model predicted as positive, how many were actually positive?

**Use Case**: Important when **False Positives are costly** (e.g., marking a legitimate email as spam).

### 9.4 Recall (Sensitivity / True Positive Rate)

**Formula**:
$$\text{Recall} = \frac{TP}{TP + FN}$$

**Interpretation**: Of all the actual positive examples, how many did the model correctly identify?

**Use Case**: Important when **False Negatives are costly** (e.g., missing a cancerous tumor).

### 9.5 F1-Score

**Formula**:
$$\text{F1} = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}$$

**Interpretation**: Harmonic mean of Precision and Recall. Balances both metrics. F1 is high only when both Precision and Recall are high.

### 9.6 Specificity (True Negative Rate)

**Formula**:
$$\text{Specificity} = \frac{TN}{TN + FP}$$

**Interpretation**: Of all the actual negative examples, how many did the model correctly identify?

**Relationship**: $\text{Specificity} = 1 - \text{False Positive Rate}$

### Summary Table

| Metric | Formula | Question Answered |
|---|---|---|
| **Accuracy** | $(TP+TN) / \text{Total}$ | How often is the model correct overall? |
| **Precision** | $TP / (TP+FP)$ | When it predicts positive, how often is it right? |
| **Recall** | $TP / (TP+FN)$ | How many actual positives did it find? |
| **F1-Score** | $2 \times (P \times R)/(P+R)$ | Balance of Precision and Recall |
| **Specificity** | $TN / (TN+FP)$ | How many actual negatives did it find? |

### Example Calculation

**Confusion Matrix**:

|  | Pred: 1 | Pred: 0 |
|---|---|---|
| Actual: 1 | TP = 40 | FN = 10 |
| Actual: 0 | FP = 5 | TN = 45 |

- **Accuracy** = $(40+45)/(40+45+5+10) = 85/100 = 0.85$
- **Precision** = $40/(40+5) = 40/45 = 0.89$
- **Recall** = $40/(40+10) = 40/50 = 0.80$
- **F1** = $2 \times (0.89 \times 0.80)/(0.89+0.80) = 0.84$
- **Specificity** = $45/(45+5) = 45/50 = 0.90$

---

## 10. Multiclass Classification (One-vs-All)

Logistic Regression is inherently binary. For $K > 2$ classes:

**Strategy**: Train $K$ separate binary classifiers.

1. **Classifier 1**: Class 1 vs. All Others → $h_\theta^{(1)}(x)$
2. **Classifier 2**: Class 2 vs. All Others → $h_\theta^{(2)}(x)$
3. ...
4. **Classifier K**: Class K vs. All Others → $h_\theta^{(K)}(x)$

**Prediction**: Choose the class $k$ with the highest probability:
$$\hat{y} = \arg\max_k h_\theta^{(k)}(x)$$

---

**Previous Topic:** [← 03. Multivariate Regression](03_Multivariate_Regression.md)
