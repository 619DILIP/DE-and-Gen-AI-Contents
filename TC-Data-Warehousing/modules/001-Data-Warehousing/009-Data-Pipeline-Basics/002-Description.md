## What Is a Data Pipeline?

A data pipeline is the automated process that moves data from a source to a destination, applying whatever extraction, transformation, and loading steps are needed along the way. This is the practical implementation of the ETL or ELT concepts covered earlier, put into an actual running system.

At its simplest, a pipeline can be described in three stages:

```text
Extract  →  Transform  →  Load
```

Each stage can be as simple as a few lines of code, or as complex as a distributed system processing terabytes of data, but the underlying stages remain conceptually the same regardless of scale.

---

## Batch vs Streaming Pipelines

Pipelines are generally categorized by how frequently they run and how much data they process at once.

- **Batch pipelines** run on a schedule, for example once per hour or once per day, processing a defined chunk of data collected since the last run. Most data warehousing pipelines are batch pipelines, since business reporting rarely needs updates more frequently than that.
- **Streaming pipelines** process data continuously, as it is generated, often with only seconds of delay. These are used when near real time information is required, such as fraud detection or live monitoring dashboards.

Batch pipelines are simpler to build and reason about, and they are the more common starting point for most data warehousing use cases.

---

## A Simple Batch Pipeline in Python

Consider a scenario where raw sales data arrives as a CSV file, and it needs to be cleaned and loaded into a database table.

```python
import csv
import sqlite3

def extract(file_path):
    with open(file_path, "r") as f:
        reader = csv.DictReader(f)
        return list(reader)

def transform(rows):
    cleaned = []
    for row in rows:
        # skip rows missing required fields
        if not row.get("quantity") or not row.get("revenue"):
            continue
        cleaned.append({
            "product_id": row["product_id"],
            "quantity": int(row["quantity"]),
            "revenue": float(row["revenue"])
        })
    return cleaned

def load(rows, db_path):
    connection = sqlite3.connect(db_path)
    cursor = connection.cursor()
    cursor.execute("""
        CREATE TABLE IF NOT EXISTS sales (
            product_id TEXT,
            quantity INTEGER,
            revenue REAL
        )
    """)
    for row in rows:
        cursor.execute(
            "INSERT INTO sales (product_id, quantity, revenue) VALUES (?, ?, ?)",
            (row["product_id"], row["quantity"], row["revenue"])
        )
    connection.commit()
    connection.close()

raw_rows = extract("daily_sales.csv")
clean_rows = transform(raw_rows)
load(clean_rows, "warehouse.db")
```

This small example demonstrates the same three stages found in production pipelines: pulling raw data in, cleaning and validating it, and writing the finished result into a structured destination.

---

## Handling Failure

A pipeline that assumes every run will succeed perfectly is fragile. Real pipelines account for common failure points:

- Source data that is missing, malformed, or in an unexpected format.
- A destination system that is temporarily unavailable.
- Partial failures, where some rows load successfully and others do not.

A common practice is to log which rows failed and why, rather than allowing a single bad row to stop the entire pipeline from completing. In the example above, rows with missing `quantity` or `revenue` values are skipped rather than causing the whole pipeline to crash.

---

## Scheduling

Most batch pipelines are set up to run automatically rather than being triggered manually every time. A pipeline might be configured to run every night at a fixed time, so that a warehouse is always up to date with the previous day's data by the time analysts begin work the next morning. Dedicated orchestration tools exist specifically to manage this scheduling, along with handling retries and dependencies between multiple pipeline steps, though a simple pipeline like the one above can also be scheduled using basic system level tools.
