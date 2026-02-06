# 01. Linear Algebra for Machine Learning

Linear Algebra is the branch of mathematics concerning linear equations and their representations in vector spaces and through matrices. In the context of Machine Learning, it serves as the primary language for defining algorithms and manipulating data.

## Table of Contents
1. [Linear Equations](#1-linear-equations)
2. [Vectors](#2-vectors)
3. [Vector Addition & Scalar Multiplication](#3-vector-addition--scalar-multiplication)
4. [Dot Product](#4-dot-product)
5. [Euclidean Norm (L2 Norm)](#5-euclidean-norm-l2-norm)
6. [Cosine Similarity](#6-cosine-similarity)
7. [Euclidean Distance](#7-euclidean-distance)
8. [Matrix Operations](#8-matrix-operations-multiplication-transpose-inverse)
9. [Eigenvalues and Eigenvectors](#9-eigenvalues-and-eigenvectors)

---

## 1. Linear Equations

A linear equation is an algebraic equation where each term is either a constant or the product of a constant and a single variable. There are no exponents or roots involved with the variables. Geometrically, these equations represent lines in 2D space, planes in 3D space, and hyperplanes in higher-dimensional spaces. In ML, we often deal with systems of linear equations to find relationships between input variables (features) and an output target.

### Formula
-   **Slope-Intercept Form**: $y = mx + c$
-   **General ML Form**: $y = w_1x_1 + w_2x_2 + \dots + w_nx_n + b$
    -   $y$: Output / Prediction
    -   $x_i$: Input features
    -   $w_i$: Weights (parameters)
    -   $b$: Bias

### Application in Machine Learning
-   **Linear Regression**: This algorithm attempts to model the relationship between two or more variables by fitting a linear equation to observed data. It finds the coefficients ($w$) that minimize the difference between the predicted line and the actual data points.
-   **Perceptrons**: The simplest unit of a neural network computes a linear equation ($z = w \cdot x + b$) before deciding whether to "fire" or not.

### Example Problem

**Question**: Solve for $y$ given the equation $y = 3x_1 - 2x_2 + 5$, where $x_1 = 4$ and $x_2 = 1$.

**Solution**:
1.  Substitute the values: $y = 3(4) - 2(1) + 5$
2.  Compute terms: $y = 12 - 2 + 5$
3.  Sum: $y = 15$


**Answer**: $y = 15$

---

## 2. Vectors

A vector is a mathematical object that has both a magnitude (size) and a direction. In computer science and ML, we typically think of a vector simply as an ordered list (or 1-dimensional array) of numbers. Each number in the vector usually corresponds to a specific characteristic or feature of a data point.

### Notation
$v = [v_1, v_2, \dots, v_n]$ where $v \in \mathbb{R}^n$

### Application in Machine Learning
-   **Data Storage**: A single row in a dataset is a vector. For example, a customer can be represented as `[age, income, debt_score]`.
-   **Feature Engineering**: Transforming raw data (like text or images) into numerical vectors allows algorithms to process them. An image is flattened into a vector of pixel intensities; a sentence is converted into a vector of word counts or embeddings.

### Example Problem

**Question**: Create a feature vector for a car with attributes: Speed=200, Price=5000, Seats=4.

**Solution**:
1.  Map attributes to an ordered list.
2.  Vector $x = [\text{Speed}, \text{Price}, \text{Seats}]$.
3.  $x = [200, 5000, 4]$.


**Answer**: $x = [200, 5000, 4]$

---

## 3. Vector Addition & Scalar Multiplication

-   **Vector Addition**: We add vectors component-wise. This geometrically represents chaining two movements together (Head-to-Tail method).
-   **Scalar Multiplication**: Scaling a vector by a real number (scalar) stretches or shrinks the vector's magnitude without changing its direction (unless the scalar is negative, which reverses it).

### Formulas
-   **Addition**: $A + B = [a_1+b_1, a_2+b_2, \dots]$
-   **Scalar Mult**: $c \cdot V = [c \cdot v_1, c \cdot v_2, \dots]$

### Application in Machine Learning
-   **Parameter Updates (Gradient Descent)**: The core learning step $W_{new} = W_{old} - \alpha \nabla J$ involves both scalar multiplication (multiplying the gradient $\nabla J$ by learning rate $\alpha$) and vector subtraction (updating the weights $W$).
-   **Moving in Feature Space**: Adding a vector to a data point shifts it to a new location in the feature space.

### Example Problem

**Question**: Let $V = [2, 5]$ and scalar $c = 3$. Find $cV$.

**Solution**:
1.  Multiply each element by 3.
2.  $3 \times 2 = 6$.
3.  $3 \times 5 = 15$.


**Answer**: $[6, 15]$

---

## 4. Dot Product

The dot product is an algebraic operation that takes two equal-length sequences of numbers and returns a single number. Geometrically, it relates to the angle between two vectors and their lengths. If the dot product is zero, the vectors are orthogonal (perpendicular).

### Formula
$A \cdot B = \sum_{i=1}^{n} a_i b_i = a_1b_1 + a_2b_2 + \dots + a_nb_n$

### Application in Machine Learning
-   **Neural Networks**: A neuron's input processing is defined as the dot product $W \cdot X + b$. This efficiently calculates the weighted sum of inputs.
-   **Efficient Computation**: Identifying similarity. If two feature vectors have a high dot product, they are strongly correlated or "aligned" in the same direction.
-   **Convolutions**: In CNNs, applying a filter to an image is fundamentally a sliding dot product operation.

### Example Problem

**Question**: Compute Dot Product of inputs $X=[1, 2, 3]$ and weights $W=[0.5, 1, -1]$.

**Solution**:
1.  Compute pairs: $(1 \times 0.5) + (2 \times 1) + (3 \times -1)$.
2.  Intermediate: $0.5 + 2 + (-3)$.
3.  Sum: $2.5 - 3 = -0.5$.


**Answer**: $-0.5$

---

## 5. Euclidean Norm (L2 Norm)

The norm of a vector represents its "size" or "length" in space, measured as the distance from the origin to the point defined by the vector. The L2 norm (Euclidean norm) is the standard geometric length.

### Formula
$||v||_2 = \sqrt{v_1^2 + v_2^2 + \dots + v_n^2}$

### Application in Machine Learning
-   **Regularization**: L2 Regularization (Ridge Regression) adds the definition of a penalty term $\lambda ||W||^2$ to the loss function. This discourages weights from becoming too large, preventing the model from becoming overly complex and overfitting the training data.
-   **Unit Vectors**: We often divide a vector by its norm to create a "unit vector" (length of 1) which preserves direction but standardizes magnitude.

### Example Problem

**Question**: Find the L2 Norm of vector $v = [-3, 4]$.

**Solution**:
1.  Square the components: $(-3)^2 = 9$, $4^2 = 16$.
2.  Sum them: $9 + 16 = 25$.
3.  Take square root: $\sqrt{25} = 5$.


**Answer**: $5$

---

## 6. Cosine Similarity

Cosine similarity measures the cosine of the angle between two vectors. It focuses purely on *orientation*, ignoring magnitude. Two vectors pointing in the exact same direction have a similarity of 1; two completely opposite vectors have -1; and orthogonal vectors have 0.

### Formula
$\text{Similarity} = \cos(\theta) = \frac{A \cdot B}{||A|| \cdot ||B||}$

### Application in Machine Learning
-   **Recommendation Systems**: In high-dimensional spaces (like user movie ratings), magnitude (number of ratings) matters less than the pattern of ratings. Cosine similarity helps find users with similar tastes even if one rates 10 movies and the other rates 100.
-   **NLP (Word Embeddings)**: It is the standard metric to transform word vectors (Word2Vec) to query semantic closeness (e.g., "King" is similar to "Queen").

### Example Problem

**Question**: Vector $A=[1, 1]$, Vector $B=[2, 2]$. Are they similar?

**Solution**:
1.  Dot Product: $(1)(2) + (1)(2) = 4$.
2.  Norm A: $\sqrt{1+1} = \sqrt{2}$.
3.  Norm B: $\sqrt{4+4} = \sqrt{8} = 2\sqrt{2}$.
4.  Denominator: $\sqrt{2} \cdot 2\sqrt{2} = 2 \cdot 2 = 4$.
5.  Result: $4 / 4 = 1$.


**Answer**: Similarity is $1.0$ (They point in the exact same direction).

---

## 7. Euclidean Distance

This is the straight-line distance between two points in multidimensional space. It is calculated using the Pythagorean theorem.

### Formula
$d(p, q) = \sqrt{\sum_{i=1}^{n} (q_i - p_i)^2}$

### Application in Machine Learning
-   **Clustering (K-Means)**: The algorithm assigns data points to the nearest cluster center based on Euclidean distance.
-   **Classification (K-Nearest Neighbors)**: To classify a new point, the algorithm measures the distance to all existing points and picks the majority class of the closest $K$ neighbors.

### Example Problem

**Question**: Distance between User A (Age 20, Score 10) and User B (Age 23, Score 14).

**Solution**:
1.  Age Diff: $23 - 20 = 3$. Score Diff: $14 - 10 = 4$.
2.  Square diffs: $3^2 = 9$, $4^2 = 16$.
3.  Sum: $25$.
4.  Square Root: $5$.


**Answer**: $5$ units.

---

## 8. Matrix Operations (Multiplication, Transpose, Inverse)

Matrices are rectangular grids of numbers. They are the core data structure for representing datasets and transformations in ML.

### 8.1 Matrix Notation
A matrix $A$ of size $m \times n$ has $m$ rows and $n$ columns:
$A = \begin{bmatrix} a_{11} & a_{12} & \dots & a_{1n} \\ a_{21} & a_{22} & \dots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{m1} & a_{m2} & \dots & a_{mn} \end{bmatrix}$

### 8.2 Matrix Multiplication
To multiply two matrices $A$ ($m \times n$) and $B$ ($n \times p$), the number of columns in $A$ must equal the number of rows in $B$. The result $C$ is of size $m \times p$.

**Formula**:
$C_{ij} = \sum_{k=1}^{n} A_{ik} \cdot B_{kj}$
(Row $i$ of $A$ dot-product with Column $j$ of $B$)

**Example**:
$\begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix} \times \begin{bmatrix} 5 & 6 \\ 7 & 8 \end{bmatrix}$

$C_{11} = (1 \times 5) + (2 \times 7) = 5 + 14 = 19$
$C_{12} = (1 \times 6) + (2 \times 8) = 6 + 16 = 22$
$C_{21} = (3 \times 5) + (4 \times 7) = 15 + 28 = 43$
$C_{22} = (3 \times 6) + (4 \times 8) = 18 + 32 = 50$

**Answer**: $\begin{bmatrix} 19 & 22 \\ 43 & 50 \end{bmatrix}$

### 8.3 Matrix Transpose ($A^T$)
Flipping a matrix over its diagonal. Rows become columns and vice versa.

**Formula**:
$(A^T)_{ij} = A_{ji}$

**Example**:
$A = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{bmatrix} \quad \Rightarrow \quad A^T = \begin{bmatrix} 1 & 4 \\ 2 & 5 \\ 3 & 6 \end{bmatrix}$

### 8.4 Matrix Inverse ($A^{-1}$)
The inverse of a matrix $A$ satisfies $A \cdot A^{-1} = I$ (Identity Matrix), where $I$ has 1s on the diagonal and 0s elsewhere.

**Formula for 2x2 Matrix**:
$A = \begin{bmatrix} a & b \\ c & d \end{bmatrix} \quad \Rightarrow \quad A^{-1} = \frac{1}{ad - bc} \begin{bmatrix} d & -b \\ -c & a \end{bmatrix}$

The term $(ad - bc)$ is called the **Determinant**. A matrix is invertible only if its determinant is non-zero.

**Example**:
$A = \begin{bmatrix} 4 & 7 \\ 2 & 6 \end{bmatrix}$

1.  Determinant: $(4)(6) - (7)(2) = 24 - 14 = 10$.
2.  Swap diagonal, negate off-diagonal: $\begin{bmatrix} 6 & -7 \\ -2 & 4 \end{bmatrix}$.
3.  Divide by determinant.

**Answer**: $A^{-1} = \begin{bmatrix} 0.6 & -0.7 \\ -0.2 & 0.4 \end{bmatrix}$

### Application in Machine Learning
-   **Batch Processing**: $Y = X \cdot W$ computes predictions for all samples at once.
-   **Normal Equation**: $\theta = (X^T X)^{-1} X^T y$ uses transpose and inverse to solve Linear Regression analytically.

---

## 9. Eigenvalues and Eigenvectors

Eigenvectors and eigenvalues are properties of square matrices. An eigenvector is a vector that does not change its direction when a linear transformation (matrix multiplication) is applied to it; it only scales. The eigenvalue is the factor by which it scales.

### Formula
$A v = \lambda v$
-   $A$: Square Matrix
-   $v$: Eigenvector
-   $\lambda$ (lambda): Eigenvalue

### Application in Machine Learning
-   **Dimensionality Reduction (PCA)**: Principal Component Analysis finds the "principal components" of the data, which are actually the eigenvectors of the covariance matrix. The eigenvalues tell us how much "information" (variance) each component holds.
-   **PageRank**: Google's original algorithm uses the eigenvector of the web graph matrix to rank page importance.

### Example Problem

**Question**: If matrix $A = \begin{bmatrix} 2 & 0 \\ 0 & 3 \end{bmatrix}$ and vector $v = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$, is $v$ an eigenvector? If so, what is $\lambda$?

**Solution**:
1.  Multiply $A \cdot v$: $\begin{bmatrix} 2 & 0 \\ 0 & 3 \end{bmatrix} \begin{bmatrix} 1 \\ 0 \end{bmatrix}$.
2.  Row 1: $(2 \times 1) + (0 \times 0) = 2$.
3.  Row 2: $(0 \times 1) + (3 \times 0) = 0$.
4.  Result is $\begin{bmatrix} 2 \\ 0 \end{bmatrix}$.
5.  Compare to original $v$: $\begin{bmatrix} 2 \\ 0 \end{bmatrix} = 2 \times \begin{bmatrix} 1 \\ 0 \end{bmatrix}$.
6.  It is a scalar multiple of $v$.

**Answer**: Yes, it is an eigenvector with eigenvalue $\lambda = 2$.

---

**Next Topic:** [02. Statistics & Probability →](02_Statistics_Probability.md)
