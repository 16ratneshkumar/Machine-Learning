# 04. Core Machine Learning Concepts (Mathematical View)

This section connects pure mathematics to specific ML components.

## Table of Contents
1. [Mean Squared Error (MSE)](#1-mean-squared-error-mse)
2. [Gradient Descent](#2-gradient-descent)
3. [Log Loss (Binary Cross Entropy)](#3-log-loss-binary-cross-entropy)
4. [Sigmoid Function](#4-sigmoid-function)
5. [Softmax](#5-softmax)
6. [Logarithm](#6-logarithm)
7. [Entropy (Information Theory)](#7-entropy-information-theory)
8. [Convex Functions](#8-convex-functions)

---

## 1. Mean Squared Error (MSE)

MSE is a "cost function" or "loss function". It quantifies how good or bad a regression model is. It calculates the average of the squared differences between the predicted values and the actual target values. We square the errors so that negative errors (guessing too low) don't cancel out positive errors (guessing too high), and to penalize large mistakes more severely.

### Formula
$J = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$

### Application in Machine Learning
-   **Regression Evaluation**: It is the standard metric for training Linear Regression models. Minimizing MSE guarantees finding the line of best fit.
-   **Metric**: It is used to report model accuracy in specific units (e.g., "Our house price predictions are off by an average of \$5000 squared").

### Example Problem

**Question**: True Value $y=10$. Predicted $\hat{y}=14$.

**Solution**:
1.  Difference: $10 - 14 = -4$.
2.  Square it: $(-4)^2 = 16$.


**Answer**: Error contribution is 16.

---

## 2. Gradient Descent

Gradient Descent is the universal optimization algorithm in machine learning. Think of it as being lost on a mountain in the dark. You feel the slope of the ground under your feet (the gradient) and take a small step downhill. You repeat this until you reach the bottom (the minimum error).

### Formula
$\theta_{new} = \theta_{old} - \alpha \nabla J(\theta)$
-   $\theta$: The model weights.
-   $\alpha$: Learning rate (how big a step to take).
-   $\nabla J$: Gradient of the cost function.

### Application in Machine Learning
-   **Model Training**: It is used to train almost all Deep Learning models (CNNs, Transformers) and many standard ML models. Without it, we couldn't solve for the millions of parameters in modern AI.

### Example Problem

**Question**: Current weight $w=2$. Gradient is $+3$. Learning Rate $\alpha=0.1$.

**Solution**:
1.  Adjustment: $0.1 \times 3 = 0.3$.
2.  Direction: Subtract (go opposite to gradient).
3.  New Weight: $2 - 0.3 = 1.7$.


**Answer**: $1.7$

---

## 3. Log Loss (Binary Cross Entropy)

Log Loss is the cost function used for binary classification (Yes/No problems). Unlike MSE, which deals with distances, Log Loss deals with probabilities. It penalizes incorrect confident predictions exponentially. If you predict 100% probability of "Yes" and the answer is "No", the error is infinite.

### Formula
$J = -[y \log(\hat{y}) + (1-y) \log(1-\hat{y})]$

### Application in Machine Learning
-   **Classification Training**: It is the standard loss function for Logistic Regression and Neural Network classifiers. It forces the model to not just be "right", but to be "confidently right" about the correct class.

### Example Problem

**Question**: True Label $y=1$. Model predicts $\hat{y}=0.1$ (Model thinks it's 0).

**Solution**:
1.  Term 1: $1 \cdot \log(0.1)$. (Assume $\log_{10}$ for simplicity, though ML uses $\ln$). $\log_{10}(0.1) = -1$.
2.  Term 2: $(1-1) \dots = 0$.
3.  Formula: $-(-1) = 1$.


**Answer**: 1 (High penalty).

---

## 4. Sigmoid Function

The Sigmoid function is an S-shaped curve that maps *any* real number input into a range between 0 and 1. This property makes it perfect for interpreting outputs as probabilities.

### Formula
$\sigma(z) = \frac{1}{1 + e^{-z}}$

### Application in Machine Learning
-   **Activation Function**: In Logic Regression, it transforms a raw linear score ($z$) into a probability ($p$) that belongs to class 1.
-   **Neural Gates**: Used in LSTM networks to control how much information flows through a gate (0 = closed, 1 = open).

### Example Problem

**Question**: Input $z$ is very large positive number ($z \to \infty$).

**Solution**:
1.  $e^{-\infty}$ approaches 0.
2.  Denominator becomes $1 + 0 = 1$.
3.  Result $1/1 = 1$.


**Answer**: Output approaches 1.

---

## 5. Softmax

Softmax is the multi-class equivalent of Sigmoid. If you have 10 possible classes (e.g., digits 0-9), Softmax takes 10 raw scores and normalizes them into 10 probabilities that sum up to exactly 1.0.

### Formula
$P(Class_i) = \frac{e^{z_i}}{\sum e^{z_j}}$

### Application in Machine Learning
-   **Output Layer**: It is the standard final layer for multi-class classification networks (e.g., ImageNet classification). It allows the model to select the single most likely category.

### Example Problem

**Question**: Logits $[2, 0, 1]$. Which is max probability?

**Solution**:
1.  $e^2 \approx 7.4$ (Largest score).
2.  Softmax preserves order, so the largest input gives largest probability.


**Answer**: Class 1 (Index 0).

---

## 6. Logarithm

A logarithm asks "to what power must, I raise a base to get this number?". In ML, we usually use the Natural Logarithm (base $e$). The key property is that it is monotonically increasing (preserves order) and turns multiplication into addition.

### Application in Machine Learning
-   **Numerical Stability**: Multiplying many small probabilities (e.g., $0.01 \times 0.01 \dots$) results in floating-point underflow (computer reads it as 0). Summing their logs ($\log(0.01) + \dots$) keeps the numbers in a manageable range.
-   **Optimization**: Maximizing the "Likelihood" is mathematically equivalent to maximizing the "Log-Likelihood", but the derivative of the sum of logs is much easier to compute than the derivative of a product.

### Example Problem

**Question**: Convert multiplication $A \times B$ to addition using logs.

**Solution**:
1.  Apply log: $\log(AB)$.
2.  Rule: $\log(A) + \log(B)$.


**Answer**: $\log A + \log B$

---

## 7. Entropy (Information Theory)

Entropy measures the amount of uncertainty or "surprise" in a probability distribution. A fair coin flip has high entropy (maximum uncertainty). A coin that always lands on Heads has zero entropy (zero surprise).

### Formula
$H(X) = - \sum_{i} P(x_i) \log_2 P(x_i)$

### Application in Machine Learning
-   **Decision Trees**: Algorithms like ID3 or C4.5 use "Information Gain" (Reduction in Entropy) to decide which feature to split on. They choose the split that creates the most "pure" (low entropy) child nodes.
-   **Cross-Entropy Loss**: In classification, we want our predicted probability distribution to match the actual distribution. Minimizing cross-entropy makes the predictions certain and correct.

### Example Problem

**Question**: A coin is slightly biased: $P(H) = 0.8$, $P(T) = 0.2$. Calculate Entropy (using $\log_2$).
(Note: $\log_2(0.8) \approx -0.32$, $\log_2(0.2) \approx -2.32$)

**Solution**:
1.  Term 1 (Heads): $0.8 \times -0.32 = -0.256$.
2.  Term 2 (Tails): $0.2 \times -2.32 = -0.464$.
3.  Sum: $-0.256 + -0.464 = -0.72$.
4.  Negate: $-(-0.72) = 0.72$.


**Answer**: $0.72$ bits. (Lower than a fair coin, which is 1.0).

---

## 8. Convex Functions

A function is convex if a line segment between any two points on its graph lies above or on the graph. Visually, it looks like a "bowl" shape. The key property is that a convex function has only one minimum, which is also the global minimum.

### Visual Test
If you can draw a line between any two points on the curve and that line never goes *below* the curve, the function is convex.

### Application in Machine Learning
-   **Guaranteed Global Minimum**: If your loss function is convex (like MSE for Linear Regression), Gradient Descent is guaranteed to find the best possible solution, not just a local one.
-   **Why Deep Learning is Hard**: The loss surfaces of Neural Networks are *non-convex*, meaning they have many local minima and saddle points, making optimization challenging.

### Example Problem

**Question**: Is the function $f(x) = x^2$ convex?

**Solution**:
1.  The function is a parabola opening upwards.
2.  Any line drawn between two points on the curve will be above the curve.
3.  It has a single minimum at $x=0$.

**Answer**: Yes, it is a convex function.

---

**Previous Topic:** [← 03. Calculus](03_Calculus.md)
