# Cumulative for NumPy

<details><summary>Learning Objectives</summary>

# Learning Objectives
After completing this module, associates should be able to:

- Describe what NumPy is and why it is used in Python
- Create and work with NumPy arrays (`ndarray`)
- Perform basic indexing, slicing, and filtering on arrays
- Use vectorized operations and aggregations instead of manual loops
- Understand, at a high level, how NumPy fits into the data / visualization ecosystem

</details>

<details><summary>Description</summary>

# What is NumPy?

**NumPy** (Numerical Python) is a core library for numerical computing in Python.  
Its main feature is the **`ndarray`**, an efficient, multi-dimensional array object.

Compared to plain Python lists, NumPy arrays:

- Store data in **contiguous memory**, which allows fast operations in compiled C/Fortran code
- Support **vectorized operations** (doing math on entire arrays at once)
- Provide many built-in **numerical functions** (statistics, linear algebra, random numbers, etc.)

NumPy is a foundational library: tools like **pandas**, **matplotlib**, **scikit-learn**, and many deep learning frameworks depend on it.

</details>

<details><summary>Real World Application</summary>

# Real World Application for NumPy

NumPy is used anywhere you need fast, structured numerical work in Python, for example:

- **Data analysis** – efficient manipulation of numeric columns before loading into pandas
- **Machine learning and AI** – manipulating feature vectors, matrices, and tensors
- **Scientific computing** – simulations, numerical methods, and experimentation
- **Image and signal processing** – images, audio, and sensor data are often represented as NumPy arrays

In practice, NumPy often sits at the bottom of a Python data stack:

- Data might be loaded from files (CSV, images, sensors) into **NumPy arrays**
- Those arrays are then passed to **pandas** for tabular analysis, **matplotlib** for plotting, or an ML library for modeling

A strong grasp of NumPy makes it easier to learn and reason about these higher-level tools.

</details>

<details><summary>Implementation</summary>

# Implementation

## Installing and Importing NumPy

In most environments, NumPy can be installed with:

```bash
pip install numpy
```

The common convention is to import NumPy with the alias `np`:

```python
import numpy as np
```

## Creating Arrays

You can create arrays from Python lists or from NumPy helper functions:

```python
import numpy as np

# From a Python list
a = np.array([1, 2, 3, 4])

# From a list of lists (2D array)
matrix = np.array([[1, 2, 3],
                   [4, 5, 6]])

# Helper functions
zeros = np.zeros((2, 3))     # 2x3 array of 0.0
ones = np.ones((3, 3))       # 3x3 array of 1.0
rng  = np.arange(0, 10, 2)   # [0, 2, 4, 6, 8]
```

Useful attributes:

```python
print(a.shape)   # (4,)  -> 1D array with 4 elements
print(matrix.ndim)  # 2  -> 2D array
print(matrix.dtype) # data type (e.g., int64, float64)
```

## Vectorized Operations

NumPy is designed so that most operations work on **entire arrays**:

```python
import numpy as np

a = np.array([1, 2, 3, 4])
b = np.array([10, 20, 30, 40])

print(a + b)     # [11 22 33 44]
print(a * 2)     # [2 4 6 8]
print(b / a)     # [10. 10. 10. 10.]
```

Instead of writing manual loops in Python, you let NumPy apply the operation in optimized C code, which is both **shorter to write** and usually **much faster**.

## Indexing, Slicing, and Boolean Filtering

You can index and slice arrays similarly to lists, but with more power:

```python
import numpy as np

data = np.array([5, 10, 15, 20, 25])

print(data[0])      # 5  (first element)
print(data[1:4])    # [10 15 20]  (slice)
```

Boolean masks allow filtering:

```python
mask = data > 10          # array([False, False,  True,  True,  True])
print(data[mask])         # [15 20 25]
```

This pattern—**build a condition, then index with it**—is very common in data work.

## Aggregations

NumPy provides many aggregation methods:

```python
import numpy as np

values = np.array([1, 2, 3, 4, 5])

print(values.sum())     # 15
print(values.mean())    # 3.0
print(values.min())     # 1
print(values.max())     # 5
```

For 2D arrays, you can aggregate by **axis**:

```python
matrix = np.array([[1, 2, 3],
                   [4, 5, 6]])

print(matrix.sum())          # 21 (all elements)
print(matrix.sum(axis=0))    # [5 7 9]   (column sums - axis=0 operates down the rows (column-wise))
print(matrix.sum(axis=1))    # [6 15]    (row sums - axis=1 operates across the columns (row-wise))
```

</details>

<details><summary>Summary</summary>

# Summary

* **NumPy** is a core numerical computing library in Python, built around the `ndarray` type
* NumPy arrays store data efficiently and support **vectorized operations** for fast math
* You create arrays from Python lists or helper functions like `np.zeros`, `np.ones`, and `np.arange`
* Indexing, slicing, and boolean masks allow powerful ways to select and filter data
* Aggregation methods such as `.sum()`, `.mean()`, and `.max()` make it easy to compute statistics
* NumPy underpins many other data and visualization libraries like **pandas** and **matplotlib**

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>