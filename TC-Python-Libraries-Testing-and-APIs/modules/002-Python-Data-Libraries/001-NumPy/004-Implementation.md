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