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