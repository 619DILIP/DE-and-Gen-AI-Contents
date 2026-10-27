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