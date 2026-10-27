<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Explain what Pandas provides beyond NumPy and when to reach for it.
- Distinguish a Series from a DataFrame and describe the role of the index.
- Load data from CSV and other sources, and inspect it before working with it.
- Select rows and columns using `loc` and `iloc`, and filter with boolean conditions.
- Handle missing data using detection, removal, and filling strategies.
- Apply grouping and aggregation to summarize data.
- Join two DataFrames and choose the appropriate join type.

</details>

<details><summary>Description</summary>

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

</details>

<details><summary>Real World Application</summary>

## Pandas in a Data Pipeline

In the transform stage of a pipeline, Pandas is often the tool doing the work. A typical sequence reads raw data from a source, inspects and validates it, cleans column names and types, handles missing values according to an agreed rule, joins in reference data, aggregates to the required grain, and writes the result to a destination.

That sequence maps directly onto the extract, transform, load structure covered in the data warehousing material. Where the pipeline module described the stages conceptually, Pandas is frequently what the transform stage actually consists of, particularly for datasets that fit comfortably in memory on one machine. For volumes beyond that, the same logical operations are expressed in a distributed framework instead, which is why the concepts transfer even when the tool changes.

</details>

<details><summary>Implementation</summary>

## Installing and Importing

```text
pip install pandas
```

```python
import pandas as pd
```

The `pd` alias is the universal convention.

---

## A Full Worked Example

Working through a realistic cleaning and summarizing task end to end.

```python
import pandas as pd

# --- Load ---
orders = pd.DataFrame({
    "order_id":    [1, 2, 3, 4, 5, 6],
    "customer_id": [101, 102, 101, 103, 102, 104],
    "product":     ["Widget", "Gadget", "Widget", "Doohickey", "Widget", "Gadget"],
    "quantity":    [2, 1, 5, 3, None, 2],
    "unit_price":  [10.0, 25.0, 10.0, 8.5, 10.0, 25.0],
    "order_date":  ["2024-01-15", "2024-01-16", "2024-02-03",
                    "2024-02-11", "2024-02-20", "2024-03-01"],
})

customers = pd.DataFrame({
    "customer_id": [101, 102, 103, 105],
    "name":        ["Maria", "James", "Priya", "Ken"],
    "region":      ["West", "East", "West", "North"],
})

# --- Inspect ---
print(orders.info())
print(orders.isna().sum())        # quantity has one missing value

# --- Clean ---
# Convert the date column from text to a real datetime type
orders["order_date"] = pd.to_datetime(orders["order_date"])

# Decide on the missing quantity. Dropping is chosen here because
# an invented quantity would distort revenue figures.
orders = orders.dropna(subset=["quantity"])
orders["quantity"] = orders["quantity"].astype(int)

# --- Derive ---
orders["revenue"] = orders["quantity"] * orders["unit_price"]
orders["month"] = orders["order_date"].dt.to_period("M")

# --- Join ---
before = len(orders)
enriched = pd.merge(orders, customers, on="customer_id", how="left")
print(f"rows before: {before}, after: {len(enriched)}")

# customer 104 has no matching record, so region is NaN
enriched["region"] = enriched["region"].fillna("Unknown")

# --- Aggregate ---
by_region = enriched.groupby("region").agg(
    total_revenue=("revenue", "sum"),
    order_count=("order_id", "count"),
    avg_quantity=("quantity", "mean"),
).reset_index()

print(by_region)

by_month = enriched.groupby("month")["revenue"].sum()
print(by_month)
```

Two details in that example are worth pointing out. The `how="left"` join keeps every order even when no customer record matches, which is usually the right choice when orders are the fact being measured. And the row count check before and after the join is the habit that catches duplicate keys silently inflating the data.

---

## Working with Dates

Date handling is common enough to deserve its own note. Once a column is converted with `pd.to_datetime`, the `.dt` accessor exposes date components.

```python
df["order_date"] = pd.to_datetime(df["order_date"])

df["order_date"].dt.year
df["order_date"].dt.month
df["order_date"].dt.day_name()
df["order_date"].dt.to_period("M")     # monthly period, useful for grouping
```

Filtering by date range then works naturally:

```python
mask = (df["order_date"] >= "2024-02-01") & (df["order_date"] < "2024-03-01")
february = df[mask]
```

---

## Adding and Modifying Columns

```python
df["total"] = df["quantity"] * df["unit_price"]
df["is_bulk"] = df["quantity"] > 10
df = df.rename(columns={"unit_price": "price"})
df = df.drop(columns=["temporary_column"])
```

For conditional values, `np.where` handles the simple two way case, and `pd.cut` handles binning into ranges:

```python
import numpy as np

df["size"] = np.where(df["quantity"] > 10, "large", "small")

df["band"] = pd.cut(
    df["revenue"],
    bins=[0, 50, 200, float("inf")],
    labels=["low", "medium", "high"],
)
```

---

## Writing Data Out

```python
df.to_csv("output.csv", index=False)
df.to_json("output.json", orient="records")
df.to_sql("summary_table", connection, if_exists="replace", index=False)
```

Passing `index=False` to `to_csv` is almost always wanted, since otherwise the row index is written as an unnamed extra column that causes confusion when the file is read back.

---

## Steps to Follow

1. Load the data and immediately run `.info()` and `.isna().sum()`.
2. Fix column types, particularly dates, before deriving anything from them.
3. Decide on a missing data strategy deliberately, and record the reasoning.
4. Derive new columns from clean inputs, not from raw ones.
5. Check row counts before and after any join.
6. Aggregate to the grain the output actually needs.
7. Write out with `index=False` unless the index carries meaning.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Pandas builds on NumPy to handle labeled, mixed type tabular data.
- A Series is one labeled column; a DataFrame is a table of Series sharing an index.
- The index identifies rows and is used to align data during operations.
- `loc` selects by label and includes the slice endpoint; `iloc` selects by position and excludes it.
- Missing data is detected with `isna` and handled by dropping or filling, which is a judgment call rather than a technical one.
- `groupby` with aggregation maps directly onto SQL's `GROUP BY`.
- `merge` performs joins using the same inner, left, right, and outer types as SQL.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
