## Installing pytest

```text
pip install pytest
```

## Project Layout

```text
project/
    calculator.py
    test_calculator.py
```

## Writing Tests with pytest

```python
# test_calculator.py
from calculator import add, divide
import pytest

def test_add():
    assert add(2, 3) == 5

def test_divide():
    assert divide(10, 2) == 5

def test_divide_by_zero():
    with pytest.raises(ZeroDivisionError):
        divide(10, 0)
```

## Running the Tests

```text
pytest
```

Adding `-v` produces a more detailed report listing each test by name.

```text
pytest -v
```

## The Same Tests Using unittest

```python
import unittest
from calculator import add, divide

class TestCalculator(unittest.TestCase):

    def test_add(self):
        self.assertEqual(add(2, 3), 5)

    def test_divide(self):
        self.assertEqual(divide(10, 2), 5)

    def test_divide_by_zero(self):
        with self.assertRaises(ZeroDivisionError):
            divide(10, 0)

if __name__ == "__main__":
    unittest.main()
```

## Steps to Follow

1. Install pytest, or use unittest with no installation required.
2. Create a test file named with a `test_` prefix.
3. Write test functions, each named with a `test_` prefix.
4. Run the test suite from the project directory.
5. Read the output and fix any reported failures.