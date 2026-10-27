## Introduction to Spark SQL

Spark SQL is a Spark module designed for working with structured and
semi-structured data.

It allows users to:

- Execute SQL queries
- Work with DataFrames
- Integrate relational processing with Spark programs
- Access multiple data sources using a unified interface

Spark SQL bridges the gap between traditional SQL-based systems and
distributed data processing.

---

## Why Spark SQL?

Before Spark SQL, users relied heavily on Hive for SQL-based processing
on Hadoop. Spark SQL was introduced to:

- Provide better performance than Hive MapReduce execution
- Integrate SQL with Spark applications
- Enable advanced optimization through Catalyst Optimizer
- Support modern data formats like Parquet and ORC

Spark SQL combines:

- Declarative SQL queries
- Programmatic DataFrame API
- Distributed execution engine

---

## How Spark SQL Works

Spark SQL operates on top of the Spark Engine.

It introduces:

### 1. DataFrame API

A distributed collection of data organized into named columns.

- Similar to a table in a relational database
- Supports SQL-style operations
- Optimized internally by Catalyst

### 2. Dataset API

- Strongly typed version of DataFrame (primarily in Scala/Java)
- Combines RDD benefits with Spark SQL optimization

### 3. Catalyst Optimizer

Catalyst is Spark SQL's query optimizer.

It performs:

- Logical plan optimization
- Predicate pushdown
- Constant folding
- Join reordering
- Physical plan selection

---

## Spark SQL Libraries

1.  Data Source API -- Connect to various storage systems
2.  DataFrame API -- Structured data manipulation
3.  SQL Interpreter -- Executes SQL queries
4.  Catalyst Optimizer -- Query optimization engine
5.  Tungsten Engine -- Improves memory and CPU efficiency

---

## Key Features of Spark SQL

- Integration with Spark applications
- Uniform data access across formats
- Hive compatibility
- JDBC/ODBC connectivity
- High performance and scalability
- Support for structured and semi-structured data

---

## Supported Data Sources

Spark SQL supports:

- Parquet
- ORC
- JSON
- CSV
- JDBC
- Hive tables
- Kafka (via structured streaming)