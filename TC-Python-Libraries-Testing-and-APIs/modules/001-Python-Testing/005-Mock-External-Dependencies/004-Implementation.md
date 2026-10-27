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