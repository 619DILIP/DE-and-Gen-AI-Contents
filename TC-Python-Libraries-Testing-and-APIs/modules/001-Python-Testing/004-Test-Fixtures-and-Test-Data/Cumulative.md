<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Explain what a fixture is and the problem it solves.
- Create fixtures using the `@pytest.fixture` decorator.
- Choose an appropriate fixture scope for a given resource.
- Use `yield` to handle setup and teardown in one place.
- Share fixtures across test files using `conftest.py`.
- Run a single test against many input cases using parameterization.
- Load test data from external JSON and CSV files.

</details>

<details><summary>Description</summary>

## The Problem Fixtures Solve

Tests need something to work with. A test for an order-processing function needs orders. A test for a database function needs a connection. Written directly, that preparation ends up repeated in every test:

```python
def test_total():
    orders = [{"id": 1, "amount": 100.0}, {"id": 2, "amount": 250.0}]
    assert calculate_total(orders) == 350.0

def test_average():
    orders = [{"id": 1, "amount": 100.0}, {"id": 2, "amount": 250.0}]
    assert calculate_average(orders) == 175.0
```

The duplication is the problem. Changing the sample data means changing it everywhere, and it is easy to update one and miss another.

A fixture moves that preparation into one named function, which tests then request by name.

```python
import pytest

@pytest.fixture
def sample_orders():
    return [
        {"id": 1, "amount": 100.0},
        {"id": 2, "amount": 250.0},
    ]

def test_total(sample_orders):
    assert calculate_total(sample_orders) == 350.0

def test_average(sample_orders):
    assert calculate_average(sample_orders) == 175.0
```

The mechanism is worth noticing. The test declares `sample_orders` as a parameter, and `pytest` matches that name to the fixture and passes the result in. The test never calls the fixture directly. This is dependency injection: the test states what it needs, and the framework supplies it.

---

## Fixture Scope

By default, a fixture runs again for every test that requests it, so each test gets fresh data. That is usually what is wanted, since it prevents one test affecting another.

Some resources are expensive to create, though. Opening a database connection for every one of two hundred tests wastes a great deal of time. Scope controls how often a fixture is recreated.

| Scope | Created | Suits |
|---|---|---|
| `function` (default) | Once per test | Data that tests might modify |
| `class` | Once per test class | Shared setup within a group |
| `module` | Once per test file | Moderately expensive resources |
| `session` | Once per entire test run | Expensive, read only resources |

```python
@pytest.fixture(scope="session")
def database_connection():
    conn = connect_to_test_database()
    return conn
```

The trade off is real. A wider scope is faster but means tests share the same object, so one test modifying it can affect another. Fresh data per test is the safer default, and scope should be widened deliberately rather than routinely.

---

## Setup and Teardown with yield

Many resources need cleaning up afterward: a file deleted, a connection closed, a table dropped. A fixture handles both halves using `yield`. Everything before the `yield` is setup, everything after is teardown.

```python
import pytest
from pathlib import Path

@pytest.fixture
def sample_csv():
    # Setup
    path = Path("temp_orders.csv")
    path.write_text("order_id,amount\n1,100.0\n2,250.0\n")

    # Hand the value to the test
    yield path

    # Teardown
    path.unlink()
```

The teardown runs even when the test fails, which is the important property. Cleanup written at the end of a test body is skipped when an assertion fails partway through, leaving stray files or open connections behind. A fixture does not have that problem.

---

## Fixtures Depending on Fixtures

A fixture can request another fixture in exactly the way a test does, which allows setup to be composed rather than duplicated.

```python
@pytest.fixture
def connection():
    conn = connect_to_test_database()
    yield conn
    conn.close()

@pytest.fixture
def orders_table(connection):
    connection.execute("CREATE TABLE orders (id INT, amount REAL)")
    yield connection
    connection.execute("DROP TABLE orders")

def test_insert_order(orders_table):
    orders_table.execute("INSERT INTO orders VALUES (1, 100.0)")
    result = orders_table.execute("SELECT COUNT(*) FROM orders").fetchone()
    assert result[0] == 1
```

The test requests only `orders_table`, and `pytest` works out that it needs `connection` first, creating them in order and tearing them down in reverse.

---

## Sharing Fixtures with conftest.py

Fixtures needed across several test files belong in a file named `conftest.py`. Tests in the same directory and below can use them without importing anything.

```text
tests/
    conftest.py          fixtures available to everything below
    test_orders.py
    test_customers.py
    pipeline/
        conftest.py      additional fixtures for these tests only
        test_transform.py
```

The absence of an import is deliberate and can be confusing at first. A fixture appearing in a test with no visible definition is almost always defined in a `conftest.py` somewhere up the directory tree.

---

## Parameterization

A fixture supplies the same data to many tests. Parameterization does the opposite: it runs the same test against many different inputs.

```python
import pytest

@pytest.mark.parametrize("value,expected", [
    (100.0, "small"),
    (500.0, "medium"),
    (5000.0, "large"),
    (0.0, "small"),
])
def test_categorize_order(value, expected):
    assert categorize(value) == expected
```

That runs four separate tests. Each is reported individually, so a failure identifies exactly which input broke rather than just saying the test failed.

This is a considerably better fit than a loop inside a single test. A loop stops at the first failure and hides how many other cases would also have failed.

---

## Externalizing Test Data

Small amounts of data belong in the test. Larger sets are better held in a file, which keeps the test readable and lets cases be added without touching code.

| Approach | Suits |
|---|---|
| Inline values | A handful of simple cases |
| Fixtures | Structured data shared across tests |
| External files | Large sets, or sets edited by non developers |

JSON suits nested or structured data. CSV suits tabular cases and can be edited in a spreadsheet, which matters when someone other than a developer is contributing test cases.

</details>

<details><summary>Real World Application</summary>

## Testing a Transformation Function

A pipeline's transform stage is one of the most valuable things to test, because it contains the business rules and it is where a silent error corrupts data rather than crashing visibly.

Testing it well means running it against many input cases: valid rows, rows with missing fields, rows with the wrong type, boundary values, and empty input. Parameterization covers that set concisely, and holding the cases in a CSV file means a data analyst who understands the rules can add a case without writing Python.

Fixtures handle the surrounding setup. A fixture creating a temporary database, populating it, and dropping it afterward means each test runs against a known state and leaves nothing behind, which is what makes a test suite safe to run repeatedly on any machine.

</details>

<details><summary>Implementation</summary>

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

</details>

<details><summary>Summary</summary>

In this module, we learned:

- A fixture holds shared test setup in one place, and tests request it by declaring its name as a parameter.
- Scope controls how often a fixture is recreated, trading speed against isolation between tests.
- `yield` splits a fixture into setup and teardown, with teardown running even when a test fails.
- Fixtures can depend on other fixtures, which are resolved and torn down in the correct order.
- `conftest.py` shares fixtures across test files without any import.
- Parameterization runs one test against many inputs, reporting each case separately.
- Test data can be externalized to JSON or CSV so cases can be added without changing code.

These techniques are what make a test suite maintainable once it grows beyond a handful of simple assertions.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
