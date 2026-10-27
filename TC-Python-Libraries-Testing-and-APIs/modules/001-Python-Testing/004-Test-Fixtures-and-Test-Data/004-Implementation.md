## A Complete Fixture Setup

```python
# tests/conftest.py
import pytest
import sqlite3
from pathlib import Path

@pytest.fixture(scope="session")
def data_dir():
    """Location of test data files, created once per run."""
    return Path(__file__).parent / "data"

@pytest.fixture
def connection():
    """A fresh in-memory database for each test."""
    conn = sqlite3.connect(":memory:")
    conn.row_factory = sqlite3.Row
    yield conn
    conn.close()

@pytest.fixture
def orders_table(connection):
    """A connection with an empty orders table ready to use."""
    connection.execute("""
        CREATE TABLE orders (
            order_id INTEGER PRIMARY KEY,
            amount   REAL,
            region   TEXT
        )
    """)
    connection.commit()
    return connection

@pytest.fixture
def populated_orders(orders_table):
    """The orders table with sample rows already inserted."""
    orders_table.executemany(
        "INSERT INTO orders VALUES (?, ?, ?)",
        [(1, 100.0, "WEST"), (2, 250.0, "EAST"), (3, 75.0, "WEST")],
    )
    orders_table.commit()
    return orders_table
```

Using an in-memory database is worth noting. It is created and discarded entirely in memory, so tests are fast and leave no files behind.

```python
# tests/test_orders.py
def test_table_starts_empty(orders_table):
    count = orders_table.execute("SELECT COUNT(*) FROM orders").fetchone()[0]
    assert count == 0

def test_regional_total(populated_orders):
    total = populated_orders.execute(
        "SELECT SUM(amount) FROM orders WHERE region = 'WEST'"
    ).fetchone()[0]
    assert total == 175.0
```

Neither test imports anything or creates a database. Each requests the state it needs by name.

---

## Parameterizing a Validation Function

```python
import pytest
from pipeline import clean_amount

@pytest.mark.parametrize("raw,expected", [
    ("100.00",   100.0),
    ("  250.5 ", 250.5),
    ("1,000.00", 1000.0),
    ("0",        0.0),
])
def test_clean_amount_valid(raw, expected):
    assert clean_amount(raw) == expected

@pytest.mark.parametrize("raw", ["", "abc", None, "12.34.56"])
def test_clean_amount_rejects_invalid(raw):
    with pytest.raises(ValueError):
        clean_amount(raw)
```

Splitting valid and invalid cases into two parameterized tests keeps each one focused on a single expected behavior.

---

## Loading Cases from a CSV File

```text
tests/data/amount_cases.csv
```

```text
raw,expected
100.00,100.0
250.5,250.5
"1,000.00",1000.0
0,0.0
```

```python
import csv
import pytest
from pathlib import Path

def load_cases(filename):
    path = Path(__file__).parent / "data" / filename
    with open(path, newline="") as f:
        return [(r["raw"], float(r["expected"])) for r in csv.DictReader(f)]

@pytest.mark.parametrize("raw,expected", load_cases("amount_cases.csv"))
def test_clean_amount_from_file(raw, expected):
    assert clean_amount(raw) == expected
```

Adding a case now means adding a row to the CSV. No Python changes at all.

---

## Loading Structured Data from JSON

```python
import json
import pytest
from pathlib import Path

@pytest.fixture(scope="session")
def sample_orders(data_dir):
    with open(data_dir / "orders.json") as f:
        return json.load(f)

def test_every_order_has_required_fields(sample_orders):
    required = ["order_id", "amount", "region"]
    for order in sample_orders:
        for field in required:
            assert field in order, f"order {order} is missing {field}"

def test_no_negative_amounts(sample_orders):
    assert all(o["amount"] >= 0 for o in sample_orders)
```

The assertion message in the first test names the offending record, which turns a failure from "something was missing" into a specific, actionable report.

---

## Steps to Follow

1. Identify setup repeated across tests, and move it into a fixture.
2. Give the fixture a descriptive name, since tests request it by that name.
3. Leave the scope at `function` unless the resource is genuinely expensive.
4. Use `yield` whenever anything needs cleaning up afterward.
5. Move fixtures needed by more than one file into `conftest.py`.
6. Use parameterization rather than looping inside a test, so each case is reported separately.
7. Move large or frequently edited case sets into a JSON or CSV file.