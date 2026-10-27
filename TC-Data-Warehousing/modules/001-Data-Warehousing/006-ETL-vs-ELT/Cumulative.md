<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Define ETL and explain each of its three stages.
- Define ELT and explain how it reorders those stages.
- Compare ETL and ELT in terms of where transformation happens and why that matters.
- Identify which approach is better suited to a given scenario.
- Explain how modern cloud data warehouses have influenced the shift toward ELT.

</details>

<details><summary>Description</summary>

## Getting Data Into a Warehouse

Data does not arrive in a data warehouse on its own. It has to be extracted from source systems, transformed into the correct structure, and loaded into its final destination. ETL and ELT are two different orderings of this same basic process, and the difference between them has real consequences for performance and system design.

---

## ETL: Extract, Transform, Load

ETL performs these three steps in order:

1. **Extract**: Pull raw data out of source systems, such as an application database or an external file.
2. **Transform**: Clean, reshape, and standardize that data, for example converting date formats, removing duplicates, or joining data from multiple sources, all before it is loaded anywhere permanent.
3. **Load**: Write the finished, transformed data into the destination warehouse.

```text
Source Data → Extract → Transform (in a separate processing system) → Load → Warehouse
```

The key detail in ETL is that transformation happens outside the warehouse, in a separate processing system, before the data ever touches its final destination. This was the standard approach for decades, largely because older warehouse systems were not powerful enough to handle heavy transformation work themselves.

---

## ELT: Extract, Load, Transform

ELT reorders the last two steps:

1. **Extract**: Pull raw data out of source systems, exactly as in ETL.
2. **Load**: Load that raw, untransformed data directly into the warehouse first.
3. **Transform**: Perform the cleaning and reshaping afterward, using the processing power of the warehouse itself.

```text
Source Data → Extract → Load (raw data goes straight into the warehouse) → Transform (inside the warehouse)
```

ELT became practical as modern cloud data warehouses, such as Snowflake, Redshift, and BigQuery covered earlier, grew powerful enough to handle large scale transformation work directly, removing the need for a separate transformation system.

---

## Why the Order Matters

| | ETL | ELT |
|---|---|---|
| Where transformation happens | Separate processing system, before loading | Inside the warehouse, after loading |
| Raw data availability | Not stored, only transformed data is loaded | Raw data is available in the warehouse alongside transformed data |
| Flexibility | Transformation logic must be decided upfront | Transformation logic can be changed or reapplied later, since raw data is retained |
| Infrastructure needs | Requires a separate transformation system | Relies on the compute power of the warehouse itself |

Because ELT retains the raw data inside the warehouse, it offers more flexibility. If a business requirement changes and a different transformation is needed, that transformation can be rerun against the raw data already sitting in the warehouse, rather than needing to re extract everything from the original source systems again.

---

## Choosing Between ETL and ELT

ETL remains a reasonable choice when source data needs significant cleaning or sensitive data needs to be filtered or masked before it ever reaches the warehouse, for compliance or security reasons. ELT is generally favored in modern cloud environments where the warehouse itself has ample compute power, and where retaining raw data provides useful flexibility for future analysis.

</details>

<details><summary>Real World Application</summary>

## Modern Cloud Pipelines

Many organizations building new data pipelines today default to ELT specifically because their chosen warehouse platform, whether Snowflake, Redshift, or BigQuery, is powerful enough to handle transformation directly, and because keeping raw data on hand supports future analysis that was not anticipated when the pipeline was originally built. A common modern pattern loads raw data into the warehouse first, then uses SQL based transformation tools running inside the warehouse to progressively clean and reshape that data into the fact and dimension tables analysts ultimately query.

</details>

<details><summary>Implementation</summary>

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

</details>

<details><summary>Summary</summary>

In this module, we learned:

- ETL extracts data, transforms it in a separate system, then loads the finished result into the warehouse.
- ELT extracts data, loads it into the warehouse first, then transforms it using the warehouse's own compute power.
- ELT retains raw data in the warehouse, offering more flexibility for future or changed transformation needs.
- ETL is still useful when data must be cleaned or filtered before it reaches the warehouse, often for compliance reasons.
- The rise of powerful cloud data warehouses has driven a general shift toward ELT in modern pipelines.

Understanding this movement of data sets up the final data warehousing topic, which looks at building a simple pipeline in practice.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
