In this module, we learned:

- Pandas builds on NumPy to handle labeled, mixed type tabular data.
- A Series is one labeled column; a DataFrame is a table of Series sharing an index.
- The index identifies rows and is used to align data during operations.
- `loc` selects by label and includes the slice endpoint; `iloc` selects by position and excludes it.
- Missing data is detected with `isna` and handled by dropping or filling, which is a judgment call rather than a technical one.
- `groupby` with aggregation maps directly onto SQL's `GROUP BY`.
- `merge` performs joins using the same inner, left, right, and outer types as SQL.