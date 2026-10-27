## Evaluating a Platform

A structured comparison usually covers the same categories for each candidate platform.

1. Which cloud provider is the organization already using?
2. What is the expected data volume, and how quickly will it grow?
3. How many concurrent users will query the warehouse?
4. What is the team's existing SQL and platform experience?
5. How does the pricing model align with expected usage patterns?

## Connecting to a Warehouse from Python

The connection pattern is similar across platforms, differing mainly in the connector library used.

```python
# Example connection pattern using environment variables
import os

config = {
    "account":   os.environ.get("WAREHOUSE_ACCOUNT"),
    "user":      os.environ.get("WAREHOUSE_USER"),
    "password":  os.environ.get("WAREHOUSE_PASSWORD"),
    "database":  "sales_warehouse",
    "schema":    "public"
}
```

Credentials are read from environment variables rather than written directly into the code.

## Running a Query

```python
def run_query(connection, sql):
    cursor = connection.cursor()
    cursor.execute(sql)
    rows = cursor.fetchall()
    cursor.close()
    return rows
```

## Cost Awareness

Because several platforms bill based on data scanned, limiting the columns and rows a query touches has a direct cost effect.

```sql
-- Scans every column
SELECT * FROM warehouse.orders;

-- Scans only what is needed
SELECT order_id, amount
FROM warehouse.orders
WHERE order_date >= '2024-01-01';
```