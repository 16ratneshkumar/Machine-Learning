# 12. Gradient Descent

## 1. Overview
Gradient descent is a first-order iterative optimization algorithm used to minimize a differentiable objective function. In machine learning and deep learning, it is the primary method for training models by iteratively updating parameters to reduce the training loss.

## 2. Core Concepts
- **Optimization Strategy:** Parameters are adjusted in the opposite direction of the gradient of the loss function.
- **Learning Rate ($\eta$):** A scalar hyperparameter that determines the step size at each iteration.
  - **Oversized ($\eta$ is too large):** The updates may overshoot the minimum, leading to oscillation or divergence.
  - **Undersized ($\eta$ is too small):** The algorithm requires an excessive number of iterations to converge, risking entrapment in local minima.
- **Scalability:** Gradient-based methods scale efficiently to models with millions of parameters and massive datasets where closed-form analytical solutions are computationally infeasible.

## 3. Algorithm Variants
- **Batch Gradient Descent:** Computes the gradient over the entire dataset before executing an update.
- **Stochastic Gradient Descent (SGD):** Estimates the gradient using a single sample or a mini-batch, providing stochastic approximations that drastically improve computational speed.
- **Backpropagation:** An efficient algorithm utilized in neural networks to compute gradients ($\nabla_\theta$) across multiple layers via the chain rule.

## 4. Mathematical Formulation

### Parameter Update Rule
The fundamental update equation at iteration $t$ is:

$$ \theta_{t+1} = \theta_t - \eta \nabla_\theta \mathcal{L}(\theta_t) $$

**Where:**
- $\theta$: Model parameters (e.g., weights and biases)
- $\eta$: Learning rate
- $\nabla_\theta \mathcal{L}(\theta_t)$: Gradient of the loss function with respect to $\theta$ at step $t$

## 5. Algorithmic Workflow

```text
    Initial Parameters (θ_0)
            |
            v
+--> Compute Loss: L(θ)
|           |
|           v
|    Compute Gradient: ∇_θ L(θ)
|           |
|           v
|    Update: θ_new = θ - η * ∇_θ L(θ)
|           |
+-----------+ (Iterate until convergence)
            |
            v
    Optimized Parameters (θ*)
```

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](11_linear_regression_multiple_variables.md) | [Next](13_overfitting_and_regularization.md)
