## Introduction to Aggregate Functions

Aggregate functions compute summary values from a collection of rows.

They are commonly used to:

- Count records
- Calculate averages
- Find minimum and maximum values
- Compute sums
- Determine distinct counts

When applied with groupBy(), they generate results per group.

---

## Common Aggregate Functions in Spark

---

Function Description

---

| Function                | Description                                            |
| ----------------------- | ------------------------------------------------------ |
| count()                 | Returns total number of rows                           |
| countDistinct()         | Returns number of distinct values                      |
| approx_count_distinct() | Approximate distinct count (faster for large datasets) |
| sum()                   | Returns sum of values                                  |
| avg()                   | Returns average value                                  |
| min()                   | Returns minimum value                                  |
| max()                   | Returns maximum value                                  |
| first()                 | Returns first value                                    |
| last()                  | Returns last value                                     |
| collect_list()          | Collects values including duplicates                   |
| collect_set()           | Collects unique values                                 |

---

## Grouped Aggregations

Using:

groupBy("column").agg()

Example use cases:

- Total sales per department
- Average salary per team
- Distinct product count per category

---

## When to Use approx_count_distinct()

For very large datasets where exact distinct counting is expensive.

It provides faster approximate results using probabilistic algorithms.

---

## Combining Multiple Aggregations

Multiple aggregate functions can be used together in agg():

df.groupBy("department").agg(sum("salary"), avg("salary"))

---

## Null Handling

Most aggregate functions ignore null values by default.

Functions like first() and last() support ignoreNulls parameter.