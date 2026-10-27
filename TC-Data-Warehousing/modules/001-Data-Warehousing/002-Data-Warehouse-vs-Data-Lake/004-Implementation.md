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