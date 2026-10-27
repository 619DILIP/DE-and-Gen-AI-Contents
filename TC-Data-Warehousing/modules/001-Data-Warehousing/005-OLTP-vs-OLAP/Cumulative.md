<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Define OLTP and OLAP.
- Explain the type of workload each system is optimized for.
- Compare OLTP and OLAP systems across key dimensions such as query type and data structure.
- Identify examples of each type of system.
- Explain why a single system rarely serves both purposes well.

</details>

<details><summary>Description</summary>

## Two Very Different Jobs

Databases exist to serve very different purposes depending on what they are used for. OLTP and OLAP describe two broad categories of database workload, and understanding the difference explains why organizations often run separate systems for their day to day operations and their reporting and analysis.

---

## OLTP: Online Transaction Processing

OLTP systems are designed to handle a high volume of short, simple transactions in real time. Examples include placing an order, updating a bank balance, or checking a customer into a hotel. These systems prioritize:

- Speed for individual, small operations.
- Accuracy and consistency, since these transactions often involve money or inventory.
- Support for many simultaneous users performing different operations at once.

A typical OLTP query touches a small number of rows, for example fetching a single customer's record or updating one order's status. The database structure behind an OLTP system, covered in earlier SQL modules through concepts like normalization, is designed to avoid duplicate data and support fast, precise updates.

---

## OLAP: Online Analytical Processing

OLAP systems are designed for the opposite kind of workload: large scale queries that aggregate and analyze data across many records, often spanning long periods of time. Examples include calculating total revenue by region over the past year, or identifying the best selling product category across every store.

OLAP systems prioritize:

- Fast performance on queries that scan large volumes of historical data.
- Support for complex aggregation, filtering, and grouping.
- Read heavy access patterns, since OLAP systems are queried far more often than they are updated.

A data warehouse is a form of OLAP system. The data modeling approaches used in warehousing, such as star schemas, exist specifically to make this kind of large scale aggregate query fast.

---

## Comparing OLTP and OLAP

| | OLTP | OLAP |
|---|---|---|
| Purpose | Run day to day operations | Support analysis and reporting |
| Query type | Small, simple, frequent | Large, complex, less frequent |
| Data volume touched per query | Few rows | Many rows, often millions |
| Data structure | Normalized, minimizes redundancy | Denormalized, optimized for read performance |
| Users | Applications, front line staff | Analysts, decision makers |
| Update frequency | Constant, real time | Periodic, in batches |

---

## Why Not Use One System for Both?

It is technically possible to run analytical queries directly against an OLTP system, but doing so at scale creates problems. Large, complex OLAP style queries can consume enough resources to slow down the very transactions the OLTP system exists to process quickly. This is one of the central reasons organizations maintain a separate data warehouse: it allows analytical workloads to run without any risk of degrading the performance of live operational systems.

</details>

<details><summary>Real World Application</summary>

## An Airline Example

An airline's booking system is a clear example of OLTP. When a passenger books a flight, the system needs to instantly check seat availability, reserve the seat, and process payment, all as one fast, reliable transaction. Millions of these small transactions happen across the system every day.

Separately, the airline's business analysts want to know which routes were most profitable last quarter, or how booking patterns shift around holidays. Running that kind of query directly against the live booking system risks slowing it down during a busy travel period. Instead, booking data is regularly copied into a data warehouse, an OLAP system, where these large scale analytical queries can run without touching the live booking system at all.

</details>

<details><summary>Implementation</summary>

## An OLTP Style Query

OLTP queries touch a small number of rows and run constantly.

```sql
-- Fetch one customer record
SELECT customer_id, name, email
FROM customers
WHERE customer_id = 501;

-- Update one order
UPDATE orders
SET status = 'shipped'
WHERE order_id = 1001;
```

## An OLAP Style Query

OLAP queries scan and aggregate large volumes of data.

```sql
SELECT
    region,
    EXTRACT(MONTH FROM sale_date) AS month,
    SUM(revenue) AS total_revenue,
    COUNT(*) AS transaction_count
FROM warehouse_sales
WHERE sale_date >= '2024-01-01'
GROUP BY region, EXTRACT(MONTH FROM sale_date)
ORDER BY region, month;
```

## Comparing Table Design

An OLTP table is normalized to avoid duplication.

```sql
CREATE TABLE orders (
    order_id     INT PRIMARY KEY,
    customer_id  INT REFERENCES customers(customer_id),
    order_date   DATE,
    amount       DECIMAL(10, 2)
);
```

An OLAP table is often denormalized, repeating descriptive values to avoid joins during analysis.

```sql
CREATE TABLE sales_analysis (
    sale_id        INT,
    customer_name  VARCHAR(100),
    customer_region VARCHAR(50),
    product_name   VARCHAR(100),
    product_category VARCHAR(50),
    sale_date      DATE,
    revenue        DECIMAL(10, 2)
);
```

## Steps to Follow

1. Identify whether a query serves an operation or an analysis.
2. Check how many rows the query needs to touch.
3. Route small, frequent, precise queries to the operational system.
4. Route large, aggregate, historical queries to the warehouse.
5. Avoid running heavy aggregate queries against a live operational database.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- OLTP systems handle high volumes of fast, simple, real time transactions.
- OLAP systems handle large scale analytical queries over historical data.
- OLTP data is typically normalized, while OLAP data is typically denormalized for read performance.
- Running heavy analytical queries against an OLTP system can degrade its performance.
- Data warehouses are a form of OLAP system, built specifically to keep analytical workloads separate from live operations.

This distinction sets up the next topic, which compares data warehouses directly against another common storage approach for large scale data, the data lake.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
