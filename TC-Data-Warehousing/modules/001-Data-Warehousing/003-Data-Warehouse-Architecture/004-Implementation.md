## Setting Up the Layers

A three tier architecture is typically implemented as separate schemas or databases, keeping each layer isolated.

```sql
CREATE SCHEMA staging;
CREATE SCHEMA warehouse;
CREATE SCHEMA reporting;
```

## Staging Table Example

Staging tables usually accept data loosely, using text columns, so that a malformed value does not cause the load to fail before it can be inspected.

```sql
CREATE TABLE staging.raw_orders (
    order_id      VARCHAR(50),
    customer_id   VARCHAR(50),
    order_date    VARCHAR(50),
    amount        VARCHAR(50),
    loaded_at     TIMESTAMP
);
```

## Warehouse Table Example

The warehouse layer enforces proper data types, after validation has occurred.

```sql
CREATE TABLE warehouse.orders (
    order_id      INT PRIMARY KEY,
    customer_id   INT,
    order_date    DATE,
    amount        DECIMAL(10, 2)
);
```

## Moving Data Between Layers

```sql
INSERT INTO warehouse.orders (order_id, customer_id, order_date, amount)
SELECT
    CAST(order_id AS INT),
    CAST(customer_id AS INT),
    CAST(order_date AS DATE),
    CAST(amount AS DECIMAL(10, 2))
FROM staging.raw_orders
WHERE order_id IS NOT NULL
  AND amount IS NOT NULL;
```

## Steps to Follow

1. Create separate schemas for staging, warehouse, and reporting.
2. Load raw source data into staging with permissive column types.
3. Validate and filter the staged data.
4. Cast values to proper types and insert into warehouse tables.
5. Clear the staging tables once the load has succeeded.