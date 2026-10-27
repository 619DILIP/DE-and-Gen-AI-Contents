## What Pandas Adds

NumPy handles numbers arranged in arrays. Real data is rarely that tidy. It has column names, mixed types across columns, missing values, and rows that mean something as a unit. A sales record has a date, a product name, a quantity, and a price, and those are four different types belonging to one row.

Pandas is built for that shape of data. It sits on top of NumPy, using NumPy arrays to store each column, while adding labeled columns, a row index, per column types, and operations that treat the table as a table: grouping, joining, reshaping, and handling missing values.

If NumPy is a matrix, Pandas is a spreadsheet or a database table, expressed in Python.

---

## Series and DataFrame

Pandas has two core structures.

A **Series** is a one dimensional labeled array. It is essentially one column, with an index attached.

```python
import pandas as pd

s = pd.Series([10, 20, 30], index=["a", "b", "c"])
print(s)
# a    10
# b    20
# c    30
# dtype: int64

print(s["b"])     # 20
```

A **DataFrame** is a two dimensional table: an ordered collection of Series sharing a common index.

```python
df = pd.DataFrame({
    "product":  ["Widget", "Gadget", "Doohickey"],
    "price":    [10.0, 25.0, 8.5],
    "quantity": [100, 40, 250],
})

print(df)
#      product  price  quantity
# 0     Widget   10.0       100
# 1     Gadget   25.0        40
# 2  Doohickey    8.5       250
```

Each column is a Series and has its own dtype. This is the key difference from a NumPy array, where one dtype applies to everything.

---

## The Index

Every DataFrame has an index, the labels identifying each row. By default it is a range of integers, but it can be anything meaningful: a date, a customer ID, a product code.

```python
df = df.set_index("product")
print(df.loc["Gadget"])
# price       25.0
# quantity    40.0
```

The index matters more than it first appears. Pandas uses it to align data during operations, so adding two Series matches values by label rather than by position. That alignment is helpful when it is intended and confusing when it is not, which is why knowing what the index holds is worth checking early.

---

## Loading and Inspecting Data

Pandas reads from many sources. CSV is the most common in a pipeline context.

```python
df = pd.read_csv("sales.csv")
df = pd.read_json("data.json")
df = pd.read_excel("report.xlsx")
df = pd.read_sql("SELECT * FROM orders", connection)
```

The `read_sql` case connects directly to the Python and SQL work covered earlier, allowing a query result to become a DataFrame in one step.

Before doing anything with loaded data, inspect it. This habit catches problems that would otherwise surface much later.

```python
df.head()          # first five rows
df.tail(3)         # last three rows
df.shape           # (rows, columns)
df.columns         # column names
df.dtypes          # type of each column
df.info()          # types, non null counts, memory usage
df.describe()      # summary statistics for numeric columns
```

`df.info()` is the single most useful of these, because it shows both the dtype and the non null count for every column at once, revealing type problems and missing data together.

---

## Selecting Data

Column selection uses bracket notation. A single name returns a Series, a list of names returns a DataFrame.

```python
df["price"]                  # Series
df[["product", "price"]]     # DataFrame
```

Row selection uses two accessors that are frequently confused:

- **`loc`** selects by label
- **`iloc`** selects by integer position

```python
df.loc[0]                    # row with index label 0
df.iloc[0]                   # first row by position
df.loc[0:2]                  # labels 0 to 2, inclusive of 2
df.iloc[0:2]                 # positions 0 and 1, exclusive of 2
df.loc[0, "price"]           # single value by label
df.loc[:, ["product"]]       # all rows, selected column
```

The inclusivity difference is the part that catches people. `loc` includes the endpoint because it is working with labels, where excluding the last one would be surprising. `iloc` excludes it, matching normal Python slicing.

---

## Filtering

Boolean filtering works as it does in NumPy, with conditions applied to columns.

```python
df[df["price"] > 10]
df[(df["price"] > 10) & (df["quantity"] < 50)]
df[df["product"].isin(["Widget", "Gadget"])]
df[df["product"].str.startswith("W")]
```

The same rules apply: parentheses around each condition, `&` and `|` rather than `and` and `or`.

The `.str` accessor is worth noting. It applies string methods across an entire column, which is how text cleaning is usually done:

```python
df["product"].str.lower()
df["product"].str.strip()
df["product"].str.replace("Doohickey", "Thing")
df["product"].str.contains("get")
```

---

## Missing Data

Real data has gaps. Pandas represents them as `NaN` and provides tools specifically for handling them.

```python
df.isna()                # boolean DataFrame, True where missing
df.isna().sum()          # count of missing values per column
df.dropna()              # drop rows with any missing value
df.dropna(subset=["price"])   # drop only where price is missing
df.fillna(0)             # replace missing with 0
df["price"].fillna(df["price"].mean())   # fill with the column mean
```

The choice between dropping and filling is a judgment call, not a technical one. Dropping loses data and can bias results if the missingness is not random. Filling invents values that were never observed. Which is appropriate depends on how much is missing, why, and what the data will be used for. Making that decision deliberately, and documenting it, matters more than which option is chosen.

---

## Grouping and Aggregation

Grouping is where Pandas becomes genuinely powerful, and it maps directly onto SQL's `GROUP BY`.

```python
sales.groupby("region")["revenue"].sum()
sales.groupby("region")["revenue"].mean()
sales.groupby(["region", "product"])["revenue"].sum()
```

The pattern is: split the data by one or more keys, apply a function to each group, and combine the results. Multiple aggregations can be applied at once:

```python
sales.groupby("region").agg({
    "revenue": "sum",
    "quantity": "mean",
    "order_id": "count",
})
```

Anyone comfortable with the SQL covered earlier will recognize this immediately. The equivalent query would be:

```sql
SELECT region, SUM(revenue), AVG(quantity), COUNT(order_id)
FROM sales
GROUP BY region;
```

---

## Joining DataFrames

Combining two tables works much as it does in SQL, with the same join types.

```python
merged = pd.merge(
    orders,
    customers,
    on="customer_id",
    how="inner",
)
```

The `how` argument takes `inner`, `left`, `right`, or `outer`, matching the SQL joins covered earlier. When the key column has different names in each table, `left_on` and `right_on` are used instead.

```python
pd.merge(orders, customers,
         left_on="cust_id", right_on="customer_id",
         how="left")
```

A frequent problem after joining is unexpected row counts. If the key is not unique in one of the tables, rows multiply. Checking `len(df)` before and after a join is a cheap way to catch it.