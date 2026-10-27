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