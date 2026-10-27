# Cumulative for pandas

<details><summary>Learning Objectives</summary>

# Learning Objectives
After completing this module, associates should be able to:

- Explain what pandas is and why it is used in data analysis
- Load, inspect, filter, and transform tabular data using `DataFrame` and `Series`
- Perform common operations such as selecting columns, filtering rows, sorting, grouping, and aggregating
- Read data from CSV files and write DataFrames back to CSV
- Understand how pandas integrates with NumPy and visualization libraries like matplotlib

</details>

<details><summary>Description</summary>

# What is pandas?

**pandas** is a powerful Python library for working with **tabular data**, similar to working with tables in Excel or SQL.

It provides two main data structures:

- **`Series`** → a single column of data  
- **`DataFrame`** → a table made of multiple Series (rows & columns)

pandas was built on top of **NumPy**, which makes it fast and efficient for data analysis and manipulation.

Key features:

- Easy loading of data from CSV, Excel, JSON, SQL, and more
- Powerful row and column filtering
- Built-in aggregation, grouping, merging, and reshaping tools
- Time series support (dates, timestamps, resampling)
- Integration with matplotlib for visualization

pandas is one of the most important tools in data science, analytics, and ETL workflows.

</details>

<details><summary>Real World Application</summary>

# Real World Application for pandas

pandas is used in almost every data-related job:

- **Data cleaning & preprocessing**  
  Removing duplicates, fixing missing values, converting data types

- **Exploratory Data Analysis (EDA)**  
  Quickly inspecting datasets: means, counts, correlations, distributions

- **Business reporting**  
  Summaries by customer, region, product, etc.

- **ETL pipelines**  
  Reading raw files → transforming → outputting cleaned results

- **Machine learning workflows**  
  Preparing data for model training (feature engineering)

- **Finance & economics**  
  Working with time-series data (prices, volumes, indicators)

Wherever tabular data exists, pandas is usually involved.

</details>

<details><summary>Implementation</summary>

# Implementation

## Installing and Importing pandas

Install with pip (if needed):

```bash
pip install pandas
```

Import using the standard alias:

```python
import pandas as pd
```

---

## Creating DataFrames

You can create a DataFrame from a Python dictionary:

```python
import pandas as pd

data = {
    "name": ["Alice", "Bob", "Carla"],
    "age": [25, 30, 29],
    "city": ["NYC", "LA", "Chicago"]
}

df = pd.DataFrame(data)
print(df)
```

Output:

```
    name  age     city
0  Alice   25      NYC
1    Bob   30       LA
2  Carla   29  Chicago
```

You’ll work with `DataFrame` objects for almost all analysis.

---

## Loading Data from CSV

Most real datasets come from files:

```python
df = pd.read_csv("sales.csv")
print(df.head())   # first 5 rows
print(df.info())   # columns and data types
```

Common helpers:

```python
df.describe()      # numerical summary
df.columns         # list of column names
df.shape           # (rows, columns)
```

---

## Selecting Columns and Filtering Rows

### Selecting a single column

```python
df["age"]
```

### Selecting multiple columns

```python
df[["name", "city"]]
```

### Filtering rows based on conditions

```python
adults = df[df["age"] > 18]
nyc_people = df[df["city"] == "NYC"]
```

Conditions can be combined:

```python
df[(df["age"] > 25) & (df["city"] == "LA")]
```

---

## Sorting, Adding Columns, and Dropping Columns

### Sorting

```python
df.sort_values("age")
df.sort_values(["city", "age"], ascending=[True, False])
```

### Adding a column

```python
df["age_plus_one"] = df["age"] + 1
```

### Removing a column

```python
df = df.drop(columns=["age_plus_one"])
```

---

## Grouping and Aggregation

Grouping allows you to summarize data by category:

```python
sales_by_city = df.groupby("city")["age"].mean()
print(sales_by_city)
```

Multiple aggregations:

```python
df.groupby("city").agg(
    avg_age=("age", "mean"),
    count=("name", "count")
)
```

---

## Merging and Joining DataFrames

Similar to SQL joins:

```python
df_customers = pd.read_csv("customers.csv")
df_sales = pd.read_csv("sales.csv")

merged = df_customers.merge(df_sales, on="customer_id", how="inner")
```

Common join types:

* `inner`
* `left`
* `right`
* `outer`

---

## Exporting DataFrames

Output a cleaned dataset:

```python
df.to_csv("cleaned_data.csv", index=False)
```

---

## Using pandas with matplotlib

Example simple visualization:

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("sales.csv")
df["amount"].plot(kind="hist", bins=20)

plt.title("Sales Distribution")
plt.xlabel("Amount")
plt.ylabel("Frequency")
plt.show()
```

This works because pandas uses matplotlib behind the scenes.

</details>

<details><summary>Summary</summary>

# Summary

* **pandas** is a core Python library for working with tabular data (rows & columns).
* The two main structures are **Series** (1D) and **DataFrame** (2D).
* You can load data from CSV, inspect it, filter it, and transform it easily.
* DataFrames support powerful operations such as grouping, merging, sorting, and aggregating.
* pandas integrates with NumPy and matplotlib, making it central to Python’s data ecosystem.
* DataFrames can be saved back to files for use in reports, ETL pipelines, or machine learning workflows.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>