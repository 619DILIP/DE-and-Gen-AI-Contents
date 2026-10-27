<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Define a data lake and explain how it differs from a data warehouse.
- Compare the two approaches based on data structure, cost, and typical use case.
- Explain the concept of schema on write versus schema on read.
- Identify which approach fits a given scenario.
- Recognize the emerging role of the data lakehouse as a hybrid approach.

</details>

<details><summary>Description</summary>

## Two Different Philosophies for Storing Large Data

A data warehouse, as covered earlier, stores structured, cleaned, integrated data, organized specifically to support business analysis. A data lake takes a different approach: it stores data in its raw, original form, structured or not, and defers the work of cleaning and organizing it until later, only when that data is actually going to be used.

---

## Structure and Format

A data warehouse requires data to be transformed into a defined structure before it is loaded, following the fact and dimension modeling approach covered in later modules. This is often called schema on write, since the structure is defined before the data is written into the system.

A data lake accepts data in almost any format: structured tables, semi structured formats like JSON, and fully unstructured data like images, audio, or raw log files. The structure is only applied later, at the point the data is read and used. This is called schema on read.

```text
Data Warehouse:  Data → Transform → Structured Storage → Query
Data Lake:       Data → Store As Is → Structure Applied When Queried
```

---

## Cost and Storage

Data lakes are typically built on low cost storage systems, such as Amazon S3, covered later in this section, which makes storing very large volumes of raw data economically practical. Data warehouses generally cost more per unit of storage, since that cost also covers the structure, indexing, and query performance the warehouse provides.

This often leads organizations to store all of their raw data cheaply in a data lake first, and only move the specific, cleaned subset of that data that is actually needed for regular business reporting into a data warehouse.

---

## Comparing the Two Approaches

| | Data Warehouse | Data Lake |
|---|---|---|
| Data format | Structured only | Structured, semi structured, and unstructured |
| Schema | Defined before loading (schema on write) | Applied when read (schema on read) |
| Cost | Higher per unit stored | Lower per unit stored |
| Primary users | Business analysts, reporting tools | Data scientists, data engineers |
| Typical use | Regular business reporting and dashboards | Exploratory analysis, machine learning, raw data archival |

---

## The Data Lakehouse

A more recent approach, known as a data lakehouse, attempts to combine the low cost, flexible storage of a data lake with the structure and query performance of a data warehouse. This is achieved through additional tooling layered on top of lake storage that adds warehouse like features, such as enforced structure and faster queries, without requiring data to be fully duplicated into a separate warehouse system. This approach is becoming increasingly common, though the underlying distinction between the raw, flexible nature of a lake and the structured, curated nature of a warehouse remains useful to understand regardless of which specific tooling an organization uses.

</details>

<details><summary>Real World Application</summary>

## Using Both Together

A large organization commonly uses both a data lake and a data warehouse, not as competing choices but as complementary systems. Raw data from every source, including data that may never be used or whose future use is not yet known, is stored cheaply in a data lake. From there, the specific data needed for regular, structured business reporting is cleaned, transformed, and loaded into a data warehouse. Data scientists exploring new questions or building machine learning models often work directly with the raw data lake, since they need flexibility and access to unstructured or exploratory data that a warehouse would not typically store.

</details>

<details><summary>Implementation</summary>

## Organizing a Data Lake

Data lakes rely on naming conventions for organization, since there is no enforced schema.

```text
s3://company-data-lake/
    raw/
        orders/year=2024/month=01/day=15/orders.json
        orders/year=2024/month=01/day=16/orders.json
    processed/
        orders/year=2024/month=01/orders.parquet
```

Partitioning folders by date allows a query to read only the relevant files rather than scanning everything.

## Writing Raw Data to a Lake

```python
import json
from datetime import datetime

def write_raw_to_lake(records, base_path):
    today = datetime.now()
    path = (
        f"{base_path}/raw/orders/"
        f"year={today.year}/month={today.month:02d}/day={today.day:02d}/"
        f"orders.json"
    )
    with open(path, "w") as f:
        for record in records:
            f.write(json.dumps(record) + "\n")
    return path
```

## Applying Schema on Read

The structure is applied only when the data is read.

```python
import json

def read_with_schema(file_path):
    results = []
    with open(file_path, "r") as f:
        for line in f:
            record = json.loads(line)
            results.append({
                "order_id": int(record["order_id"]),
                "amount": float(record["amount"]),
                "order_date": record["order_date"]
            })
    return results
```

## Steps to Follow

1. Decide whether the data needs structure immediately or can be stored raw.
2. Store raw files in a lake using a partitioned folder convention.
3. Keep the original files unchanged as a permanent record.
4. Apply structure at read time when the data is needed.
5. Load only the curated subset into a warehouse for regular reporting.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- A data lake stores raw data in its original format, while a data warehouse stores cleaned, structured data.
- Data warehouses use schema on write, applying structure before data is stored.
- Data lakes use schema on read, applying structure only when the data is queried.
- Data lakes are typically cheaper to store data in and support a wider range of formats.
- A data lakehouse is a hybrid approach combining lake style storage with warehouse style structure and performance.

With the distinction between raw and structured storage clear, the next topic looks at exactly how data is structured once it does reach a data warehouse, starting with fact and dimension tables.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
