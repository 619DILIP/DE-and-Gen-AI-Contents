## A Pipeline with Logging and Error Handling

```python
import csv
import sqlite3
import logging

logging.basicConfig(level=logging.INFO)

def extract(file_path):
    logging.info(f"Extracting from {file_path}")
    with open(file_path, "r") as f:
        return list(csv.DictReader(f))

def transform(rows):
    cleaned = []
    skipped = 0
    for row in rows:
        try:
            cleaned.append({
                "product_id": row["product_id"],
                "quantity": int(row["quantity"]),
                "revenue": float(row["revenue"])
            })
        except (ValueError, KeyError) as e:
            skipped += 1
            logging.warning(f"Skipping row: {e}")
    logging.info(f"Transformed {len(cleaned)} rows, skipped {skipped}")
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
    cursor.executemany(
        "INSERT INTO sales VALUES (?, ?, ?)",
        [(r["product_id"], r["quantity"], r["revenue"]) for r in rows]
    )
    connection.commit()
    connection.close()
    logging.info(f"Loaded {len(rows)} rows")

def run_pipeline(source, destination):
    try:
        raw = extract(source)
        clean = transform(raw)
        load(clean, destination)
        logging.info("Pipeline completed successfully")
    except Exception as e:
        logging.error(f"Pipeline failed: {e}")
        raise

run_pipeline("daily_sales.csv", "warehouse.db")
```

## Scheduling the Pipeline

On a Linux system, a pipeline can be scheduled with cron to run nightly.

```text
# Run every night at 2:00 AM
0 2 * * * /usr/bin/python3 /home/pipelines/run_pipeline.py
```

## Steps to Follow

1. Write each stage as a separate function so it can be tested independently.
2. Add logging at the start and end of each stage.
3. Handle bad rows individually rather than failing the whole run.
4. Test the pipeline against a sample file before scheduling it.
5. Schedule the pipeline and monitor its logs after the first few runs.
