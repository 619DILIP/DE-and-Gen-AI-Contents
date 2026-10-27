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
