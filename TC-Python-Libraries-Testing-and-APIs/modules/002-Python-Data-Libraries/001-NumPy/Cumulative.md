<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Explain what NumPy is and why it exists alongside Python's built in lists.
- Describe the ndarray, and the concepts of shape, dimension, and dtype.
- Create arrays in several ways and inspect their properties.
- Apply vectorized operations and explain why they are faster than loops.
- Use indexing, slicing, and boolean filtering to select data from an array.
- Explain broadcasting and predict the result of operations on differently shaped arrays.
- Apply common aggregation functions along a chosen axis.

</details>

<details><summary>Description</summary>

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

</details>

<details><summary>Real World Application</summary>

## Where NumPy Appears in Data Work

In a data pipeline, NumPy rarely appears as the top level tool. It appears underneath. When a Pandas column is summed, filtered, or multiplied, the work is happening on a NumPy array beneath the surface. Understanding that layer explains behavior that would otherwise seem arbitrary, such as why a column has a single dtype, why mixing types silently converts everything to strings, and why operations on whole columns are so much faster than looping over rows.

It also appears directly when working with numerical data that is naturally array shaped rather than table shaped: sensor readings, image data, or the numerical features fed into a machine learning model. A data engineer preparing features for a model is frequently working with NumPy arrays whether or not the code mentions NumPy explicitly.

</details>

<details><summary>Implementation</summary>

## Installing and Importing

```text
pip install numpy
```

The near universal convention is to import it as `np`. Following the convention matters, since virtually all documentation and examples assume it.

```python
import numpy as np
```

---

## Inspecting an Array

A short routine for understanding an unfamiliar array:

```python
def describe(arr):
    print("shape:", arr.shape)
    print("ndim: ", arr.ndim)
    print("dtype:", arr.dtype)
    print("size: ", arr.size)      # total number of elements
    print("min/max:", arr.min(), arr.max())

data = np.array([[1.5, 2.5], [3.5, 4.5]])
describe(data)
```

---

## A Worked Example: Sales Figures

```python
import numpy as np

# Rows are products, columns are months
sales = np.array([
    [120, 135, 150, 160],    # product A
    [ 80,  75,  90,  95],    # product B
    [200, 210, 190, 220],    # product C
])

products = np.array(["A", "B", "C"])

# Total per product, collapsing the month axis
per_product = sales.sum(axis=1)
print(per_product)              # [565 340 820]

# Total per month, collapsing the product axis
per_month = sales.sum(axis=0)
print(per_month)                # [400 420 430 475]

# Average monthly sales per product
print(sales.mean(axis=1))       # [141.25  85.   205.  ]

# Which products averaged above 100 per month
strong = sales.mean(axis=1) > 100
print(products[strong])         # ['A' 'C']

# Apply a 10 percent growth forecast to every figure
forecast = sales * 1.10

# Month over month change for each product
change = np.diff(sales, axis=1)
print(change)
# [[ 15  15  10]
#  [ -5  15   5]
#  [ 10 -20  30]]
```

The final example is worth noting: `np.diff` computes the difference between adjacent elements along an axis, which is a common need when looking at change over time and awkward to write with loops.

---

## Reshaping

Reshaping changes how the same data is organized without copying it.

```python
flat = np.arange(12)             # [0 1 2 ... 11]
grid = flat.reshape(3, 4)        # 3 rows, 4 columns
back = grid.reshape(-1)          # flatten again
```

Passing `-1` for one dimension tells NumPy to work it out from the total size, which avoids hardcoding numbers that might change.

```python
flat.reshape(2, -1)     # 2 rows, NumPy infers 6 columns
```

---

## Handling Missing Values

NumPy represents missing numeric data as `np.nan`, a special float value. It propagates through calculations, which is often not what is wanted.

```python
readings = np.array([10.0, np.nan, 12.0, 15.0])

readings.mean()          # nan, because nan contaminates the result
np.nanmean(readings)     # 12.333..., ignores the nan
```

Detecting them requires `np.isnan`, since `nan` does not equal itself:

```python
np.isnan(readings)              # [False  True False False]
readings[~np.isnan(readings)]   # [10. 12. 15.]
```

The fact that `np.nan == np.nan` evaluates to `False` is a frequent source of confusion, and the reason a dedicated function exists for the check.

---

## Steps to Follow

1. Import NumPy as `np` by convention.
2. Create or load the array, and check `.shape` and `.dtype` before anything else.
3. Prefer vectorized operations over writing loops.
4. Use boolean conditions to filter, wrapping each condition in parentheses.
5. Choose the `axis` argument deliberately, remembering it names the dimension being collapsed.
6. Check for `nan` values before computing summaries on real data.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- NumPy provides a fixed type, contiguous array that is far more efficient than a Python list for numerical work.
- An ndarray is described by its shape, number of dimensions, and single dtype.
- Vectorized operations apply across a whole array without explicit loops.
- Boolean filtering selects elements matching a condition, using `&`, `|`, and `~` with parenthesized conditions.
- Broadcasting allows operations between differently shaped arrays under defined compatibility rules.
- The `axis` argument controls the direction of an aggregation, naming the dimension being collapsed.
- Missing numeric values are represented as `np.nan` and need dedicated functions to detect and ignore.

NumPy is the foundation the next module builds on, since Pandas stores its column data as NumPy arrays.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
