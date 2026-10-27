## What is a DataFrame?

A DataFrame in Spark is a distributed collection of data organized into
named columns.

It is:

- Similar to a table in a relational database
- Similar to a DataFrame in Pandas
- Built on top of RDDs
- Optimized by the Catalyst Optimizer

Unlike RDDs, DataFrames are schema-aware, meaning they know the
structure of the data.

---

## Why Use DataFrames?

DataFrames provide:

- Better optimization through Catalyst
- Automatic query optimization
- Simplified syntax
- Integration with Spark SQL
- Improved performance compared to RDDs

---

## RDD vs DataFrame

| Feature        | RDD              | DataFrame                     |
|---------------|------------------|-------------------------------|
| Schema        | No               | Yes                           |
| Optimization  | Limited          | Catalyst Optimizer            |
| Ease of Use   | More verbose     | SQL-like operations           |
| Performance   | Slower           | Faster                        |
| API Style     | Functional       | Declarative + Functional      |

---

## Key Characteristics of DataFrames

1.  Distributed and immutable
2.  Schema-based structure
3.  Lazy evaluation
4.  Supports SQL queries
5.  Optimized execution plan

---

## Common DataFrame Operations

### Transformations

- select()
- filter()
- groupBy()
- join()
- orderBy()
- withColumn()

### Actions

- show()
- collect()
- count()
- first()

---

## Schema in DataFrames

Schema defines:

- Column names
- Data types
- Nullability

Schema helps Spark optimize queries and reduce runtime errors.

---

## Data Sources Supported

DataFrames can read data from:

- CSV
- JSON
- Parquet
- ORC
- JDBC
- Hive tables