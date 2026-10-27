In this module, we learned:

- NumPy provides a fixed type, contiguous array that is far more efficient than a Python list for numerical work.
- An ndarray is described by its shape, number of dimensions, and single dtype.
- Vectorized operations apply across a whole array without explicit loops.
- Boolean filtering selects elements matching a condition, using `&`, `|`, and `~` with parenthesized conditions.
- Broadcasting allows operations between differently shaped arrays under defined compatibility rules.
- The `axis` argument controls the direction of an aggregation, naming the dimension being collapsed.
- Missing numeric values are represented as `np.nan` and need dedicated functions to detect and ignore.

NumPy is the foundation the next module builds on, since Pandas stores its column data as NumPy arrays.