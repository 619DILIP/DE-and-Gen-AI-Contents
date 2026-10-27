<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Define a data pipeline and describe its basic stages.
- Explain the difference between batch and streaming pipelines.
- Identify common points of failure in a pipeline and why error handling matters.
- Build a simple data pipeline in Python that moves data from a raw source into a structured destination.
- Explain the concept of scheduling and why pipelines typically run automatically.

</details>

<details><summary>Description</summary>

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

A third pattern sits between the two. An **event driven** pipeline runs whenever a specific thing happens, such as a file arriving, rather than on a timetable or continuously. It gives much lower latency than a batch pipeline without the complexity of a continuously running stream, and it is a common choice when data arrives at unpredictable times. The cloud section later in this course covers a concrete implementation of this pattern.

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

</details>

<details><summary>Real World Application</summary>

## A Nightly Sales Pipeline

A retail company might run a pipeline every night that pulls the day's transaction data from its point of sale systems, cleans and standardizes it, and loads it into the fact and dimension tables of its data warehouse. By the time analysts arrive the next morning, dashboards reflect the previous day's complete sales activity. If the pipeline fails partway through, for example because one store's data file was corrupted, a well built pipeline logs that specific failure and still successfully loads data from every other store, rather than leaving the entire warehouse without any updated data for that day.

</details>

<details><summary>Implementation</summary>

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

</details>

<details><summary>Summary</summary>

In this module, we learned:

- A data pipeline automates the extract, transform, and load process covered earlier.
- Batch pipelines run on a schedule and process data in chunks, while streaming pipelines process data continuously.
- A simple pipeline can be built in Python using basic file reading, cleaning logic, and database writes.
- Robust pipelines anticipate failure and handle bad or missing data gracefully rather than crashing entirely.
- Pipelines are typically scheduled to run automatically rather than triggered manually each time.

This closes out the data warehousing content. The next section moves into cloud computing and AWS, covering how these pipelines and warehouses are commonly hosted and run in practice.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
