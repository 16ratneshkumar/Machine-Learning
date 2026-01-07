# NumPy Reference Guide

Complete reference for NumPy - the fundamental package for numerical computing in Python.

---

## Installation and Import

### Installation
```bash
pip install numpy
```

### Import
```python
import numpy as np
```

**Convention:** Always import NumPy as `np` - this is the standard convention used everywhere.

---

## Creating Arrays

### `np.array()`
**Description:** Create an array from a list or tuple  
**Syntax:** `np.array(object, dtype=None)`

```python
# 1D array
arr = np.array([1, 2, 3, 4, 5])

# 2D array
arr_2d = np.array([[1, 2, 3], [4, 5, 6]])

# With specific data type
arr_float = np.array([1, 2, 3], dtype=float)
```

---

### `np.zeros()`
**Description:** Create an array filled with zeros  
**Syntax:** `np.zeros(shape, dtype=float)`

```python
zeros_1d = np.zeros(5)           # [0. 0. 0. 0. 0.]
zeros_2d = np.zeros((3, 4))      # 3x4 array of zeros
zeros_int = np.zeros(5, dtype=int)  # Integer zeros
```

---

### `np.ones()`
**Description:** Create an array filled with ones  
**Syntax:** `np.ones(shape, dtype=float)`

```python
ones_1d = np.ones(5)             # [1. 1. 1. 1. 1.]
ones_2d = np.ones((2, 3))        # 2x3 array of ones
```

---

### `np.arange()`
**Description:** Create an array with evenly spaced values within a range  
**Syntax:** `np.arange(start, stop, step)`

```python
arr = np.arange(10)              # [0, 1, 2, ..., 9]
arr = np.arange(5, 15)           # [5, 6, 7, ..., 14]
arr = np.arange(0, 10, 2)        # [0, 2, 4, 6, 8]
arr = np.arange(1, 2, 0.1)       # [1.0, 1.1, 1.2, ..., 1.9]
```

---

### `np.linspace()`
**Description:** Create an array with evenly spaced values between start and stop  
**Syntax:** `np.linspace(start, stop, num=50)`

```python
arr = np.linspace(0, 1, 5)       # [0.0, 0.25, 0.5, 0.75, 1.0]
arr = np.linspace(0, 10, 11)     # [0, 1, 2, ..., 10]
```

---

### `np.eye()`
**Description:** Create an identity matrix (diagonal of ones)  
**Syntax:** `np.eye(N, M=None)`

```python
identity = np.eye(3)             # 3x3 identity matrix
```

---

### `np.random` Functions

#### `np.random.rand()`
**Description:** Random values in [0, 1) from uniform distribution  
**Syntax:** `np.random.rand(d0, d1, ..., dn)`

```python
random_arr = np.random.rand(3, 3)    # 3x3 random values
```

#### `np.random.randn()`
**Description:** Random values from standard normal distribution  
**Syntax:** `np.random.randn(d0, d1, ..., dn)`

```python
normal_arr = np.random.randn(3, 3)   # 3x3 normal distribution
```

#### `np.random.randint()`
**Description:** Random integers from low to high  
**Syntax:** `np.random.randint(low, high, size)`

```python
int_arr = np.random.randint(0, 10, (3, 3))  # 3x3 random integers [0, 10)
```

#### `np.random.seed()`
**Description:** Set random seed for reproducibility  
**Syntax:** `np.random.seed(seed)`

```python
np.random.seed(42)               # Same random numbers every time
```

---

## Array Attributes

### `arr.shape`
**Description:** Dimensions of the array  
**Returns:** Tuple of array dimensions

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
print(arr.shape)                 # (2, 3)
```

### `arr.size`
**Description:** Total number of elements  
**Returns:** Integer

```python
print(arr.size)                  # 6
```

### `arr.ndim`
**Description:** Number of dimensions  
**Returns:** Integer

```python
print(arr.ndim)                  # 2
```

### `arr.dtype`
**Description:** Data type of elements  
**Returns:** dtype object

```python
print(arr.dtype)                 # int64 or float64
```

---

## Array Operations

### Arithmetic Operations

```python
arr = np.array([1, 2, 3, 4, 5])

# Scalar operations
arr + 5                          # Add 5 to each element
arr - 3                          # Subtract 3 from each
arr * 2                          # Multiply each by 2
arr / 2                          # Divide each by 2
arr ** 2                         # Square each element
arr % 2                          # Modulo operation

# Array operations (element-wise)
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])

arr1 + arr2                      # [5, 7, 9]
arr1 * arr2                      # [4, 10, 18]
arr1 / arr2                      # Element-wise division
```

---

## Mathematical Functions

### `np.sqrt()`
**Description:** Square root of each element  
**Syntax:** `np.sqrt(arr)`

```python
np.sqrt(np.array([1, 4, 9, 16]))  # [1., 2., 3., 4.]
```

### `np.exp()`
**Description:** Exponential (e^x) of each element  
**Syntax:** `np.exp(arr)`

```python
np.exp(np.array([0, 1, 2]))      # [1., 2.718..., 7.389...]
```

### `np.log()`
**Description:** Natural logarithm of each element  
**Syntax:** `np.log(arr)`

```python
np.log(np.array([1, np.e, np.e**2]))  # [0., 1., 2.]
```

### `np.sin()`, `np.cos()`, `np.tan()`
**Description:** Trigonometric functions  
**Syntax:** `np.sin(arr)`, `np.cos(arr)`, `np.tan(arr)`

```python
np.sin(np.array([0, np.pi/2, np.pi]))
```

### `np.abs()`
**Description:** Absolute value of each element  
**Syntax:** `np.abs(arr)`

```python
np.abs(np.array([-1, -2, 3]))    # [1, 2, 3]
```

### `np.round()`
**Description:** Round to nearest integer or decimals  
**Syntax:** `np.round(arr, decimals=0)`

```python
np.round(np.array([1.234, 5.678]), 2)  # [1.23, 5.68]
```

---

## Statistical Functions

### `np.mean()`
**Description:** Compute the arithmetic mean  
**Syntax:** `np.mean(arr, axis=None)`

```python
arr = np.array([1, 2, 3, 4, 5])
np.mean(arr)                     # 3.0

# 2D array
arr_2d = np.array([[1, 2], [3, 4]])
np.mean(arr_2d, axis=0)          # Mean of each column: [2., 3.]
np.mean(arr_2d, axis=1)          # Mean of each row: [1.5, 3.5]
```

### `np.median()`
**Description:** Compute the median  
**Syntax:** `np.median(arr, axis=None)`

```python
np.median(np.array([1, 2, 3, 4, 5]))  # 3.0
```

### `np.std()`
**Description:** Compute the standard deviation  
**Syntax:** `np.std(arr, axis=None)`

```python
np.std(np.array([1, 2, 3, 4, 5]))     # 1.414...
```

### `np.var()`
**Description:** Compute the variance  
**Syntax:** `np.var(arr, axis=None)`

```python
np.var(np.array([1, 2, 3, 4, 5]))     # 2.0
```

### `np.min()` / `np.max()`
**Description:** Find minimum/maximum value  
**Syntax:** `np.min(arr)`, `np.max(arr)`

```python
np.min(np.array([1, 2, 3, 4, 5]))     # 1
np.max(np.array([1, 2, 3, 4, 5]))     # 5
```

### `np.sum()`
**Description:** Sum of all elements  
**Syntax:** `np.sum(arr, axis=None)`

```python
np.sum(np.array([1, 2, 3, 4, 5]))     # 15
```

### `np.cumsum()`
**Description:** Cumulative sum  
**Syntax:** `np.cumsum(arr)`

```python
np.cumsum(np.array([1, 2, 3, 4]))     # [1, 3, 6, 10]
```

---

## Indexing and Slicing

### Basic Indexing

```python
arr = np.array([10, 20, 30, 40, 50])

arr[0]                           # 10 (first element)
arr[-1]                          # 50 (last element)
arr[2]                           # 30 (third element)
```

### Slicing

```python
arr[1:4]                         # [20, 30, 40] (index 1 to 3)
arr[:3]                          # [10, 20, 30] (first 3)
arr[2:]                          # [30, 40, 50] (from index 2)
arr[::2]                         # [10, 30, 50] (every 2nd element)
arr[::-1]                        # [50, 40, 30, 20, 10] (reversed)
```

### 2D Array Indexing

```python
arr_2d = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])

arr_2d[0, 1]                     # 2 (row 0, column 1)
arr_2d[1, :]                     # [4, 5, 6] (entire row 1)
arr_2d[:, 2]                     # [3, 6, 9] (entire column 2)
arr_2d[0:2, 1:3]                 # [[2, 3], [5, 6]] (subarray)
```

### Boolean Indexing

```python
arr = np.array([1, 2, 3, 4, 5])
arr[arr > 3]                     # [4, 5] (elements > 3)
arr[arr % 2 == 0]                # [2, 4] (even elements)
```

---

## Reshaping Arrays

### `arr.reshape()`
**Description:** Change the shape of an array  
**Syntax:** `arr.reshape(new_shape)`

```python
arr = np.array([1, 2, 3, 4, 5, 6])
arr.reshape(2, 3)                # [[1, 2, 3], [4, 5, 6]]
arr.reshape(3, 2)                # [[1, 2], [3, 4], [5, 6]]
arr.reshape(-1, 1)               # Auto-calculate dimension
```

### `arr.flatten()`
**Description:** Convert to 1D array  
**Syntax:** `arr.flatten()`

```python
arr_2d = np.array([[1, 2], [3, 4]])
arr_2d.flatten()                 # [1, 2, 3, 4]
```

### `arr.T` or `arr.transpose()`
**Description:** Transpose the array  
**Syntax:** `arr.T` or `arr.transpose()`

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
arr.T                            # [[1, 4], [2, 5], [3, 6]]
```

---

## Array Manipulation

### `np.concatenate()`
**Description:** Join arrays along an axis  
**Syntax:** `np.concatenate((arr1, arr2), axis=0)`

```python
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])
np.concatenate((arr1, arr2))     # [1, 2, 3, 4, 5, 6]
```

### `np.vstack()` / `np.hstack()`
**Description:** Stack arrays vertically/horizontally  
**Syntax:** `np.vstack((arr1, arr2))`, `np.hstack((arr1, arr2))`

```python
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])
np.vstack((arr1, arr2))          # [[1, 2, 3], [4, 5, 6]]
np.hstack((arr1, arr2))          # [1, 2, 3, 4, 5, 6]
```

### `np.split()`
**Description:** Split array into multiple sub-arrays  
**Syntax:** `np.split(arr, indices_or_sections)`

```python
arr = np.array([1, 2, 3, 4, 5, 6])
np.split(arr, 3)                 # [array([1, 2]), array([3, 4]), array([5, 6])]
```

---

## Useful Functions

### `np.where()`
**Description:** Return indices where condition is true  
**Syntax:** `np.where(condition, x, y)`

```python
arr = np.array([1, 2, 3, 4, 5])
np.where(arr > 3)                # (array([3, 4]),)
np.where(arr > 3, arr, 0)        # [0, 0, 0, 4, 5]
```

### `np.unique()`
**Description:** Find unique elements  
**Syntax:** `np.unique(arr, return_counts=False)`

```python
arr = np.array([1, 2, 2, 3, 3, 3])
np.unique(arr)                   # [1, 2, 3]
np.unique(arr, return_counts=True)  # (array([1, 2, 3]), array([1, 2, 3]))
```

### `np.sort()`
**Description:** Sort array  
**Syntax:** `np.sort(arr, axis=-1)`

```python
arr = np.array([3, 1, 2, 5, 4])
np.sort(arr)                     # [1, 2, 3, 4, 5]
```

### `np.argsort()`
**Description:** Indices that would sort the array  
**Syntax:** `np.argsort(arr)`

```python
arr = np.array([3, 1, 2])
np.argsort(arr)                  # [1, 2, 0]
```

### `np.dot()`
**Description:** Dot product of two arrays  
**Syntax:** `np.dot(arr1, arr2)`

```python
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])
np.dot(arr1, arr2)               # 32 (1*4 + 2*5 + 3*6)
```

---

## Linear Algebra (np.linalg)

### `np.linalg.inv()`
**Description:** Compute matrix inverse  
**Syntax:** `np.linalg.inv(matrix)`

```python
matrix = np.array([[1, 2], [3, 4]])
np.linalg.inv(matrix)
```

### `np.linalg.det()`
**Description:** Compute determinant  
**Syntax:** `np.linalg.det(matrix)`

```python
np.linalg.det(matrix)            # -2.0
```

### `np.linalg.eig()`
**Description:** Compute eigenvalues and eigenvectors  
**Syntax:** `np.linalg.eig(matrix)`

```python
eigenvalues, eigenvectors = np.linalg.eig(matrix)
```

---

**Back to the Topic:** [Libraries & Tools](3_Libraries_and_Tools.md)
