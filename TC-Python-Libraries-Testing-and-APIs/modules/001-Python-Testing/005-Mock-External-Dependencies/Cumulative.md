<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Explain why tests should not call real external systems.
- Describe what a mock object is and what it replaces.
- Create and configure a mock using `unittest.mock`.
- Use `patch` to replace a dependency for the duration of a test.
- Verify that a mocked dependency was called correctly.
- Recognize when mocking is appropriate and when it is not.

</details>

<details><summary>Description</summary>

## The Problem with Real Dependencies

Consider a function that fetches data from an external service and stores the result:

```python
import requests

def fetch_and_store(order_id, connection):
    response = requests.get(f"https://api.example.com/orders/{order_id}")
    order = response.json()
    connection.execute(
        "INSERT INTO orders VALUES (?, ?)",
        (order["id"], order["amount"]),
    )
    return order
```

Testing this as written means making a real network call every time the test runs. That creates several problems:

- **Slow.** A network call takes far longer than the rest of the test.
- **Unreliable.** The test fails when the network is down or the service is unavailable, even though the code is correct.
- **Not repeatable.** The service may return different data on different days, so the test's result depends on something outside the test.
- **Potentially harmful.** A test that writes to a real system leaves real changes behind.

None of these are problems with the function. They are problems with testing it against real dependencies. What actually needs verifying is that the function calls the service with the right URL, handles the response correctly, and writes the right values to the database. None of that requires the service to genuinely exist.

---

## What a Mock Is

A mock is a stand-in object that takes the place of a real dependency during a test. It records how it was used and returns whatever the test tells it to return.

The term for the general category is a test double, by analogy with a stunt double: something that stands in for the real thing in situations where using the real thing is impractical.

Python's `unittest.mock` module is part of the standard library, so nothing needs installing.

```python
from unittest.mock import Mock

# Create a mock
service = Mock()

# Tell it what to return
service.get_order.return_value = {"id": 1, "amount": 100.0}

# Use it as if it were real
result = service.get_order(1)
print(result)          # {'id': 1, 'amount': 100.0}

# Ask what happened to it
print(service.get_order.called)             # True
service.get_order.assert_called_once_with(1)
```

Two things are happening. The mock returns the configured value instead of doing real work, and it records the calls made to it so the test can check them afterward.

A mock accepts any attribute or method call without being told about it in advance, which is what makes it usable as a stand-in for something complex without describing the whole thing.

---

## Patching

Creating a mock is straightforward when the dependency is passed in as an argument. It is harder when the code imports and calls something directly, as `requests.get` is called in the example above.

`patch` solves this by temporarily replacing a name for the duration of a test, then restoring it afterward.

```python
from unittest.mock import patch

@patch("mymodule.requests.get")
def test_fetch_order(mock_get):
    mock_get.return_value.json.return_value = {"id": 1, "amount": 100.0}

    result = fetch_order(1)

    assert result["amount"] == 100.0
    mock_get.assert_called_once_with("https://api.example.com/orders/1")
```

The critical detail, and the most common source of confusion, is **where** to patch. The target is the name as it is used in the module under test, not where it was originally defined. Patching `requests.get` globally often does not work, because the module under test may already hold its own reference to it. Patching `mymodule.requests.get` replaces the name the module actually looks up.

The usual rule is to patch where the object is looked up, not where it is defined.

---

## Verifying Calls

Beyond controlling what a dependency returns, mocks let a test check how it was used. This matters when the important behavior is the call itself rather than the return value.

```python
mock_db.execute.assert_called_once()
mock_db.execute.assert_called_with("INSERT INTO orders VALUES (?, ?)", (1, 100.0))
mock_db.execute.assert_not_called()

print(mock_db.execute.call_count)     # how many times
print(mock_db.execute.call_args)      # the arguments of the last call
```

For a function whose whole purpose is writing to a database, verifying that the correct insert was issued with the correct values is precisely what the test should be checking.

---

## Simulating Failure

Mocks can also be told to raise an exception, which makes error handling testable without needing the real failure to occur.

```python
mock_get.side_effect = ConnectionError("network unreachable")

def test_handles_network_failure():
    with pytest.raises(ConnectionError):
        fetch_order(1)
```

This is one of mocking's most useful applications. Waiting for a real network outage to test the network-outage path is not a workable plan; a mock makes that path testable on demand.

---

## When Not to Mock

Mocking is easy to overuse, and over-mocked tests are a recognized problem.

- **Do not mock the thing being tested.** Mocking the function under test means the test verifies the mock, not the code.
- **Do not mock what is cheap and reliable.** An in-memory database, as used with fixtures, is usually a better choice than mocking every query, because it tests the real SQL rather than an assumption about it.
- **Be cautious with heavily mocked tests.** A test where nearly everything is mocked verifies that the code calls things in a particular order, and will keep passing after a refactor that breaks real behavior.

The useful boundary is to mock what is genuinely external, slow, or unreliable, such as a network service or a third-party API, and to use real, lightweight versions of everything else.

</details>

<details><summary>Real World Application</summary>

## Testing a Pipeline Without Its Dependencies

An extraction function that pulls data from a partner's API and writes it to storage has two external dependencies, neither of which should be involved in a unit test. The partner's API should not be called on every test run, and no test should write real objects into real storage.

Mocking both allows the function's actual logic to be verified: that it requests the right endpoint, that it handles a well-formed response correctly, that it skips malformed records rather than crashing, and that it retries or raises appropriately when the service returns an error. All of that is tested in milliseconds, on any machine, with no credentials and no network.

The same reasoning applies to a function that writes to a cloud service. Mocking the client verifies that the correct call would be made, with the correct arguments, without anything actually being created.

</details>

<details><summary>Implementation</summary>

## Testing a Function with a Mocked API

```python
# extractor.py
import requests

API_BASE = "https://api.partner.example.com"

def fetch_orders(since_date):
    response = requests.get(f"{API_BASE}/orders", params={"since": since_date})
    response.raise_for_status()

    orders = []
    for record in response.json():
        if not record.get("order_id") or record.get("amount") is None:
            continue
        orders.append({
            "order_id": int(record["order_id"]),
            "amount": float(record["amount"]),
        })
    return orders
```

```python
# test_extractor.py
import pytest
from unittest.mock import patch, Mock
from extractor import fetch_orders

@patch("extractor.requests.get")
def test_fetch_orders_parses_valid_records(mock_get):
    mock_get.return_value = Mock(
        status_code=200,
        json=Mock(return_value=[
            {"order_id": "1", "amount": "100.50"},
            {"order_id": "2", "amount": "250.00"},
        ]),
    )

    result = fetch_orders("2024-01-01")

    assert len(result) == 2
    assert result[0] == {"order_id": 1, "amount": 100.50}

@patch("extractor.requests.get")
def test_fetch_orders_skips_incomplete_records(mock_get):
    mock_get.return_value = Mock(
        json=Mock(return_value=[
            {"order_id": "1", "amount": "100.00"},
            {"order_id": "", "amount": "50.00"},      # missing id
            {"order_id": "3"},                        # missing amount
        ]),
    )

    result = fetch_orders("2024-01-01")

    assert len(result) == 1
    assert result[0]["order_id"] == 1

@patch("extractor.requests.get")
def test_fetch_orders_sends_correct_request(mock_get):
    mock_get.return_value = Mock(json=Mock(return_value=[]))

    fetch_orders("2024-03-15")

    mock_get.assert_called_once_with(
        "https://api.partner.example.com/orders",
        params={"since": "2024-03-15"},
    )
```

Three different things are being verified: that valid data is parsed correctly, that invalid records are skipped rather than causing a crash, and that the request itself is built correctly. None of them touch a network.

---

## Using patch as a Context Manager

The decorator form is convenient when the whole test needs the patch. A context manager limits it to part of a test instead.

```python
from unittest.mock import patch

def test_partial_patching():
    real_result = prepare_data()          # runs normally

    with patch("extractor.requests.get") as mock_get:
        mock_get.return_value = Mock(json=Mock(return_value=[]))
        result = fetch_orders("2024-01-01")

    assert result == []
```

Outside the `with` block, the original `requests.get` is restored.

---

## Combining Mocks with Fixtures

Mocks fit naturally into the fixture pattern, which keeps repeated mock setup out of individual tests.

```python
import pytest
from unittest.mock import Mock

@pytest.fixture
def mock_api_response():
    """A mock response containing two valid orders."""
    return Mock(json=Mock(return_value=[
        {"order_id": "1", "amount": "100.00"},
        {"order_id": "2", "amount": "200.00"},
    ]))

@patch("extractor.requests.get")
def test_with_fixture(mock_get, mock_api_response):
    mock_get.return_value = mock_api_response
    assert len(fetch_orders("2024-01-01")) == 2
```

---

## Testing Error Handling

```python
import pytest
from unittest.mock import patch
from requests.exceptions import ConnectionError, HTTPError

@patch("extractor.requests.get")
def test_raises_on_connection_failure(mock_get):
    mock_get.side_effect = ConnectionError("unreachable")

    with pytest.raises(ConnectionError):
        fetch_orders("2024-01-01")

@patch("extractor.requests.get")
def test_raises_on_bad_status(mock_get):
    mock_get.return_value = Mock(
        raise_for_status=Mock(side_effect=HTTPError("500 Server Error"))
    )

    with pytest.raises(HTTPError):
        fetch_orders("2024-01-01")
```

Both failure paths are now covered, and neither required a real failure to occur.

---

## Steps to Follow

1. Identify which dependencies are genuinely external, slow, or unreliable.
2. Mock those, and use real lightweight versions of everything else.
3. Patch the name as the module under test looks it up, not where it was defined.
4. Configure return values for the responses the test needs to exercise.
5. Assert on the calls made when the call itself is the behavior being tested.
6. Use `side_effect` to simulate failures and cover error handling paths.
7. Review whether a heavily mocked test is still verifying anything meaningful.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Tests should not depend on real external systems, which are slow, unreliable, and not repeatable.
- A mock stands in for a real dependency, returning configured values and recording how it was used.
- `unittest.mock` is part of the standard library and requires no installation.
- `patch` temporarily replaces a name for the duration of a test and restores it afterward.
- Patching targets the name as the module under test looks it up, not where it was originally defined.
- Assertions on a mock can verify that a dependency was called correctly, which is often the real behavior under test.
- `side_effect` simulates failures, making error handling testable without a real outage.
- Over-mocking produces tests that verify structure rather than behavior, so real lightweight dependencies are preferable where practical.

Together with fixtures and parameterization, mocking makes it possible to test code that depends on systems the test cannot or should not reach.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
