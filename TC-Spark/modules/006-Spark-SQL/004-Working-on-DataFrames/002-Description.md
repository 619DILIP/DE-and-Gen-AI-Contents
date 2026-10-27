## Introduction

A DataFrame is a distributed collection of data organized into named
columns.

It is conceptually similar to:

- A table in a relational database
- A spreadsheet
- A Pandas DataFrame (but distributed)

DataFrames are built on top of RDDs but provide:

- Schema awareness
- Catalyst query optimization
- Improved performance
- Declarative query capabilities

---

## Why DataFrames Are Important

DataFrames:

- Provide structured data processing
- Enable SQL-like operations
- Automatically optimize execution plans
- Improve readability and maintainability of code
- Support multiple data formats

They are the primary abstraction used in modern Spark applications.

---

## Key Characteristics of DataFrames

- Distributed across cluster nodes
- Immutable
- Schema-based
- Lazy evaluation
- Optimized by Catalyst
- Supports SQL queries

---

## Common Operations in DataFrames

### Column Operations

- select()
- withColumn()
- drop()
- rename()

### Row Operations

- filter()
- where()
- limit()

### Aggregations

- groupBy()
- agg()
- count()
- sum()
- avg()

### Joins

- inner join
- left join
- right join
- full outer join

### Sorting

- orderBy()
- sort()

---

## Data Sources

DataFrames can be created from:

- CSV
- JSON
- Parquet
- ORC
- JDBC
- Hive tables
- Existing RDDs