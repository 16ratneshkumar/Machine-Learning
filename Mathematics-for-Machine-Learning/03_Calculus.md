# 03. Calculus for Machine Learning

Calculus, specifically differential calculus, allows us to model change. In Machine Learning, "learning" is essentially the process of changing the model's parameters to reduce error. Calculus tells us *how* to change them.

## Table of Contents
1. [Derivative](#1-derivative)
2. [Standard Derivative Rules](#2-standard-derivative-rules)
3. [Partial Derivative](#3-partial-derivative)
4. [Chain Rule](#4-chain-rule)
5. [Gradient](#5-gradient)
6. [Critical Points](#6-critical-points)
7. [Integrals (Basics)](#7-integrals-basics)
8. [Taylor Series](#8-taylor-series)

---

## 1. Derivative

A derivative represents the instantaneous rate of change of a function. Visually, it is the slope of the tangent line to the function's curve at a specific point. It answers: "If I nudge the input $x$ slightly, how much does the output $y$ change?"

### Formula (Power Rule)
If $f(x) = x^n$, then $f'(x) = n x^{n-1}$.

### Application in Machine Learning
-   **Sensitivity Analysis**: It tells us the sensitivity of the Loss Function to a specific weight.
-   **Optimization Loop**: To improve a model, we need to minimize error. The derivative points in the direction of steepest *increase*. Therefore, we update our parameters in the *negative* direction of the derivative to slide down the error surface.

### Example Problem

**Question**: Calculate derivative of Loss function $L(w) = w^2 - 4w$ at $w=3$.

**Solution**:
1.  Differentiate: $L'(w) = 2w - 4$.
2.  Substitute $w=3$: $2(3) - 4 = 6 - 4 = 2$.


**Answer**: Slope is 2. (Since positive, we should decrease $w$ to lower Loss).

---

## 2. Standard Derivative Rules
Here is a comprehensive list of rules used to differentiate functions.

### A. Basic Rules
1.  **Constant Rule**: $\frac{d}{dx}(c) = 0$
2.  **Power Rule**: $\frac{d}{dx}(x^n) = n x^{n-1}$
3.  **Constant Multiple**: $\frac{d}{dx}[c \cdot f(x)] = c \cdot f'(x)$
4.  **Sum/Difference**: $\frac{d}{dx}[f(x) \pm g(x)] = f'(x) \pm g'(x)$

### B. Advanced Rules
5.  **Product Rule**: $\frac{d}{dx}[u \cdot v] = u'v + uv'$
6.  **Quotient Rule**: $\frac{d}{dx}\left[\frac{u}{v}\right] = \frac{u'v - uv'}{v^2}$
7.  **Chain Rule**: $\frac{d}{dx}[f(g(x))] = f'(g(x)) \cdot g'(x)$

### C. Trigonometric Functions
-   $\frac{d}{dx}(\sin x) = \cos x$
-   $\frac{d}{dx}(\cos x) = -\sin x$
-   $\frac{d}{dx}(\tan x) = \sec^2 x$
-   $\frac{d}{dx}(\cot x) = -\csc^2 x$
-   $\frac{d}{dx}(\sec x) = \sec x \tan x$
-   $\frac{d}{dx}(\csc x) = -\csc x \cot x$

### D. Exponential & Logarithmic
-   **Exponential**: $\frac{d}{dx}(e^x) = e^x$
-   **General Exp**: $\frac{d}{dx}(a^x) = a^x \ln(a)$
-   **Natural Log**: $\frac{d}{dx}(\ln x) = \frac{1}{x}$
-   **General Log**: $\frac{d}{dx}(\log_a x) = \frac{1}{x \ln(a)}$

---

## 3. Partial Derivative

Most ML problems involve functions with millions of variables (weights), not just one. A partial derivative focuses on how the function changes as *one* specific variable changes, while pretending all other variables are frozen constants.

### Notation
$\frac{\partial f}{\partial x}$ (read "partial of f w.r.t x")

### Application in Machine Learning
-   **Training Deep Networks**: A neural network loss function depends on every single weight in the network. We compute the partial derivative of the Loss with respect to *each* weight ($\frac{\partial L}{\partial w_i}$) individually to know how to update that specific connection.

### Example Problem

**Question**: Function $z = 3x^2 + 4y$. Find $\frac{\partial z}{\partial x}$.

**Solution**:
1.  For the term $3x^2$: Power rule gives $6x$.
2.  For the term $4y$: Since we are deriving w.r.t $x$, $y$ is treated as a constant number (like 5). The derivative of a constant is 0.
3.  Sum: $6x + 0$.


**Answer**: $6x$

---

## 3. Chain Rule

The Chain Rule allows us to calculate the derivative of a composite function (a function inside another function). It states that the derivative of the whole is the derivative of the outer function multiplied by the derivative of the inner function.

### Formula
$\frac{d}{dx}[f(g(x))] = f'(g(x)) \cdot g'(x)$

### Application in Machine Learning
-   **Backpropagation**: This is the fundamental algorithm for training Neural Networks. A network is a stack of layers: Layer 3 is a function of Layer 2, which is a function of Layer 1. To find how the starting weights affect the final error, we "chain" the derivatives backward from the output layer to the input layer.

### Example Problem

**Question**: Find derivative of $y = (2x + 1)^3$.

**Solution**:
1.  Outer function: $u^3 \rightarrow 3u^2$.
2.  Inner function: $2x+1 \rightarrow 2$.
3.  Multiply: $3(2x+1)^2 \cdot 2$.


**Answer**: $6(2x+1)^2$

---

## 4. Gradient

The gradient is a vector that collects all the partial derivatives of a function into a single object. Since it contains the "slope" for every dimension, the gradient vector points in the direction of the steepest ascent (the fastest way up the hill).

### Notation
$\nabla f = \left[ \frac{\partial f}{\partial x_1}, \frac{\partial f}{\partial x_2}, \dots \right]$

### Application in Machine Learning
-   **Gradient Descent**: As the name implies, this algorithm relies entirely on this vector. We calculate the gradient of the Loss Function and move against it.
-   **Saddle Points**: The gradient helps identify different types of critical points on the complex error surface of a neural network.

### Example Problem

**Question**: $f(x, y) = 2x + 3y^2$. Find Gradient at $(1, 1)$.

**Solution**:
1.  $\frac{\partial f}{\partial x} = 2$.
2.  $\frac{\partial f}{\partial y} = 6y$. At $y=1$, value is $6$.
3.  Combine into vector.


**Answer**: $\nabla f = [2, 6]$

---

## 5. Critical Points

Critical points are locations where the derivative (slope) is zero. In a 3D landscape, these are the flat spots: peaks (maxima), valleys (minima), or plateaus (saddle points).

### Application in Machine Learning
-   **Optimization Goal**: The entire goal of training is to reach a critical point that is a local (or global) minimum of the loss function. When the gradient becomes effectively zero, the algorithm stops, assuming it has found the best possible parameters.

### Example Problem

**Question**: Find the critical point (minimum) of $y = x^2 - 4x + 4$.

**Solution**:
1.  Derivative: $2x - 4$.
2.  Set to 0: $2x - 4 = 0$.
3.  Solve: $2x = 4 \rightarrow x = 2$.


**Answer**: Critical point at $x=2$.

---

## 7. Integrals (Basics)

Integration is the reverse of differentiation. While a derivative gives you the rate of change, an integral gives you the total accumulation (the area under a curve).

### Formula (Power Rule)
$\int x^n dx = \frac{x^{n+1}}{n+1} + C$ (for $n \neq -1$)

### Standard Integral Formulas

| Function | Integral |
|---|---|
| $\int k \, dx$ | $kx + C$ |
| $\int x^n \, dx$ | $\frac{x^{n+1}}{n+1} + C$ |
| $\int \frac{1}{x} \, dx$ | $\ln|x|+C$ |
| $\int e^x \, dx$ | $e^x + C$ |
| $\int a^x \, dx$ | $\frac{a^x}{\ln a} + C$ |
| $\int \sin x \, dx$ | $-\cos x + C$ |
| $\int \cos x \, dx$ | $\sin x + C$ |
| $\int \sec^2 x \, dx$ | $\tan x + C$ |
| $\int \csc^2 x \, dx$ | $-\cot x + C$ |
| $\int \sec x \tan x \, dx$ | $\sec x + C$ |
| $\int \csc x \cot x \, dx$ | $-\csc x + C$ |
| $\int \frac{1}{\sqrt{1-x^2}} \, dx$ | $\sin^{-1} x + C$ |
| $\int \frac{1}{1+x^2} \, dx$ | $\tan^{-1} x + C$ |

### Application in Machine Learning
-   **Probability Density Functions (PDFs)**: The probability that a continuous variable lies within a range is calculated by integrating the PDF over that range. The total area under any PDF must equal 1.
-   **Expected Value**: The expected value of a continuous random variable is an integral: $E[X] = \int x \cdot f(x) dx$.

### Example Problem

**Question**: Find the integral $\int 2x dx$.

**Solution**:
1.  Apply power rule: $n=1$, so $\frac{x^{1+1}}{1+1} = \frac{x^2}{2}$.
2.  Multiply by constant: $2 \times \frac{x^2}{2} = x^2$.
3.  Add constant of integration.

**Answer**: $x^2 + C$

---

## 8. Taylor Series

A Taylor Series is a way to approximate any smooth function as an infinite sum of polynomial terms. It allows us to represent complex functions (like $e^x$ or $\sin(x)$) as simpler polynomials.

### Formula (centered at $a=0$, also called Maclaurin Series)
$f(x) = f(0) + f'(0)x + \frac{f''(0)}{2!}x^2 + \frac{f'''(0)}{3!}x^3 + \dots$

### Application in Machine Learning
-   **Second-Order Optimization**: Newton's Method uses the 2nd-order Taylor expansion to converge faster than Gradient Descent.
-   **Approximating Activation Functions**: The sigmoid or softmax function can be approximated by a polynomial for faster computation in some hardware.

### Example Problem

**Question**: Write the first 3 terms of the Taylor expansion for $f(x) = e^x$ around $x=0$.

**Solution**:
1.  $f(x) = e^x$, $f'(x) = e^x$, $f''(x) = e^x$.
2.  At $x=0$: $f(0)=1$, $f'(0)=1$, $f''(0)=1$.
3.  Substitute: $1 + 1 \cdot x + \frac{1}{2!}x^2 = 1 + x + \frac{x^2}{2}$.

**Answer**: $e^x \approx 1 + x + \frac{x^2}{2}$

---

**Previous Topic:** [← 02. Statistics & Probability](02_Statistics_Probability.md) | **Next Topic:** [04. ML Concepts →](04_ML_Concepts.md)
