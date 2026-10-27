## An ETL Approach

Transformation happens in Python, before anything is loaded.

```python
import csv

def extract(path):
    with open(path) as f:
        return list(csv.DictReader(f))

def transform(rows):
    cleaned = []
    for row in rows:
        if not row.get("amount"):
            continue
        cleaned.append({
            "order_id": int(row["order_id"]),
            "amount": round(float(row["amount"]), 2),
            "region": row["region"].strip().upper()
        })
    return cleaned

def load(rows, connection):
    cursor = connection.cursor()
    for row in rows:
        cursor.execute(
            "INSERT INTO warehouse.orders (order_id, amount, region) "
            "VALUES (%s, %s, %s)",
            (row["order_id"], row["amount"], row["region"])
        )
    connection.commit()

# ETL order
rows = extract("orders.csv")
clean = transform(rows)
load(clean, connection)
```

## An ELT Approach

Raw data is loaded first, then transformed using SQL inside the warehouse.

```python
# Extract and load raw, with no transformation
rows = extract("orders.csv")
load_raw(rows, connection)   # goes into staging.raw_orders
```

```sql
-- Transform inside the warehouse
INSERT INTO warehouse.orders (order_id, amount, region)
SELECT
    CAST(order_id AS INT),
    ROUND(CAST(amount AS DECIMAL(10,2)), 2),
    UPPER(TRIM(region))
FROM staging.raw_orders
WHERE amount IS NOT NULL;
```

## Reprocessing with ELT

Because raw data remains available, a changed rule can be reapplied without re extracting.

```sql
TRUNCATE TABLE warehouse.orders;

INSERT INTO warehouse.orders (order_id, amount, region)
SELECT
    CAST(order_id AS INT),
    CAST(amount AS DECIMAL(10,2)),
    UPPER(TRIM(region))
FROM staging.raw_orders
WHERE amount IS NOT NULL
  AND CAST(amount AS DECIMAL(10,2)) > 0;
```

## Steps to Follow

1. Determine whether the warehouse has enough compute for transformation.
2. Check whether any data must be filtered before storage for compliance reasons.
3. Choose ETL when data must be cleaned before it lands anywhere permanent.
4. Choose ELT when retaining raw data provides useful flexibility.
5. Keep transformation logic in one place so it can be reviewed and changed.
