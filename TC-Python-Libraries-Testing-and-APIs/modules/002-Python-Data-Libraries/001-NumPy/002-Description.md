## Why NumPy Exists

Python lists are flexible. A single list can hold integers, strings, objects, and other lists all at once. That flexibility has a cost: every element is a separate Python object with its own type information, scattered in memory, and every operation on a list runs through the Python interpreter one element at a time.

For numerical work on large volumes of data, that overhead dominates. NumPy solves it with a different data structure: a fixed type, contiguous block of memory, operated on by compiled code rather than interpreted loops.

```python
# Pure Python: multiply every value by 2
values = [1, 2, 3, 4, 5]
doubled = [v * 2 for v in values]

# NumPy: the same operation, applied to the whole array at once
import numpy as np
values = np.array([1, 2, 3, 4, 5])
doubled = values * 2
```

The second version is shorter, but the more important difference is that the multiplication happens inside compiled code across the entire array, rather than as a Python loop. On a handful of numbers this makes no practical difference. On millions of rows it is the difference between a query finishing in seconds and finishing in minutes.

NumPy also matters because it is foundational. Pandas, scikit-learn, and most of the scientific Python ecosystem are built on top of NumPy arrays, so understanding the array model makes those libraries much easier to reason about.

---

## The ndarray

The core NumPy object is the ndarray, an n dimensional array. Three properties describe any array:

- **shape**: a tuple giving the size along each dimension
- **ndim**: the number of dimensions
- **dtype**: the single data type shared by every element

```python
import numpy as np

a = np.array([1, 2, 3, 4])
print(a.shape)   # (4,)      one dimension, four elements
print(a.ndim)    # 1
print(a.dtype)   # int64

b = np.array([[1, 2, 3],
              [4, 5, 6]])
print(b.shape)   # (2, 3)    two rows, three columns
print(b.ndim)    # 2
```

The shared dtype is the key constraint. Unlike a Python list, every element in an array has the same type. Mixing types causes NumPy to convert everything to a type that can hold all of them:

```python
np.array([1, 2, 3.5])        # dtype float64, the integers become floats
np.array([1, 2, "three"])    # dtype <U21, everything becomes a string
```

That second case is worth noticing, because it usually indicates a data problem rather than an intention.

---

## Creating Arrays

Beyond converting a list, NumPy provides constructors for common cases.

```python
np.zeros((2, 3))          # 2x3 array filled with 0.0
np.ones(5)                # array of five 1.0 values
np.full((2, 2), 7)        # 2x2 array filled with 7
np.arange(0, 10, 2)       # [0 2 4 6 8], like range() but returns an array
np.linspace(0, 1, 5)      # [0. 0.25 0.5 0.75 1.] five evenly spaced values
np.eye(3)                 # 3x3 identity matrix
```

`arange` and `linspace` differ in what the third argument means. `arange` takes a step size and the endpoint is excluded. `linspace` takes a count and the endpoint is included by default. Confusing the two is a common early mistake.

---

## Vectorized Operations

Arithmetic between arrays, or between an array and a single value, applies element by element without any explicit loop.

```python
prices = np.array([10.0, 25.0, 8.5, 40.0])
quantities = np.array([2, 1, 5, 3])

line_totals = prices * quantities
# [20.  25.  42.5 120. ]

with_tax = line_totals * 1.08
total = line_totals.sum()
```

This style, operating on whole arrays rather than individual elements, is called vectorization. It is both faster and, once familiar, easier to read, because the code states what happens to the data rather than how to iterate over it.

Comparisons vectorize too, producing arrays of booleans:

```python
prices > 20
# [False  True False  True]
```

---

## Indexing, Slicing, and Boolean Filtering

One dimensional indexing works like a list. Two dimensional indexing takes a row and column position, separated by a comma.

```python
b = np.array([[1, 2, 3],
              [4, 5, 6]])

b[0, 2]      # 3       row 0, column 2
b[1]         # [4 5 6] the whole second row
b[:, 1]      # [2 5]   column 1 from every row
b[0:2, 0:2]  # [[1 2]
             #  [4 5]]
```

Boolean filtering is where NumPy becomes genuinely expressive. A boolean array can be used directly as an index, selecting only the positions that are `True`.

```python
values = np.array([12, 45, 7, 88, 23])

values[values > 20]        # [45 88 23]
values[values % 2 == 0]    # [12 88]
```

Conditions combine with `&` for and, `|` for or, and `~` for not. Each condition needs parentheses, because these operators bind more tightly than the comparisons:

```python
values[(values > 10) & (values < 50)]   # [12 45 23]
```

Using Python's `and` or `or` here raises an error, since those work on single truth values rather than arrays. This trips up nearly everyone once.

---

## Broadcasting

Broadcasting is how NumPy handles operations between arrays of different shapes. Rather than requiring shapes to match exactly, NumPy stretches the smaller array across the larger one where the rules allow.

The simplest case is an array and a single number:

```python
np.array([1, 2, 3]) + 10     # [11 12 13]
```

The scalar is effectively broadcast across every element. The same principle extends to arrays:

```python
matrix = np.array([[1, 2, 3],
                   [4, 5, 6]])       # shape (2, 3)

row = np.array([10, 20, 30])          # shape (3,)

matrix + row
# [[11 22 33]
#  [14 25 36]]
```

The row is applied to each row of the matrix. Two dimensions are compatible when they are equal, or when one of them is 1. Shapes are compared from the rightmost dimension backward.

```python
(3, 4) and (4,)      -> compatible, the (4,) is applied to each row
(3, 4) and (3,)      -> not compatible, raises an error
(3, 4) and (3, 1)    -> compatible, the column is applied across
```

Broadcasting is powerful, but it also means a shape mistake can silently produce a valid result of the wrong size rather than an error. Checking `.shape` when a result looks wrong is usually the fastest diagnosis.

---

## Aggregations and the Axis Argument

NumPy provides the usual summary functions, and the `axis` argument controls the direction they operate in.

```python
data = np.array([[10, 20, 30],
                 [40, 50, 60]])

data.sum()            # 210     everything
data.sum(axis=0)      # [50 70 90]     down the columns
data.sum(axis=1)      # [60 150]       across the rows
```

The mental model that helps: `axis` names the dimension being collapsed. `axis=0` collapses the rows, leaving one value per column. `axis=1` collapses the columns, leaving one value per row.

Other common aggregations follow the same pattern:

```python
data.mean(axis=0)
data.min()
data.max(axis=1)
data.std()
np.median(data)
```