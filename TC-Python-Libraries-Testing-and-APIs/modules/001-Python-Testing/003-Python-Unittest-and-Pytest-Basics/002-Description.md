## Why Use a Framework Instead of Plain Asserts?

Writing `assert` statements and calling test functions manually works for small examples, but it does not scale well. A testing framework adds structure on top of that:

- It automatically discovers and runs every test in a project.
- It reports which tests passed and which failed, with details for each failure.
- It continues running remaining tests even after one fails, instead of stopping the whole program.
- It provides additional assertion methods that give more descriptive failure messages.

Python has one framework built into the standard library, `unittest`, and one widely used third party framework, `pytest`.

---

## Testing with unittest

`unittest` is included with every Python installation, so it requires no extra setup. Tests are written as methods inside a class that inherits from `unittest.TestCase`.

```python
import unittest

def add(a, b):
    return a + b

class TestAddFunction(unittest.TestCase):

    def test_add_positive_numbers(self):
        self.assertEqual(add(2, 3), 5)

    def test_add_negative_numbers(self):
        self.assertEqual(add(-2, -3), -5)

    def test_add_zero(self):
        self.assertEqual(add(0, 5), 5)

if __name__ == "__main__":
    unittest.main()
```

Each test method name must start with `test_`, which is how `unittest` recognizes it as a test rather than a regular method. Instead of using `assert` directly, `unittest` provides methods such as:

- `assertEqual(a, b)`
- `assertTrue(condition)`
- `assertFalse(condition)`
- `assertRaises(ExceptionType)`

Running this file produces output showing how many tests ran and whether they passed, along with a traceback for any that failed.

`unittest` also provides `setUp` and `tearDown` methods, which run automatically before and after every test method in the class. These handle preparation and cleanup that would otherwise be repeated in each test.

```python
class TestOrderProcessing(unittest.TestCase):

    def setUp(self):
        # Runs before each test method
        self.orders = [
            {"id": 1, "amount": 100.0},
            {"id": 2, "amount": 250.0},
        ]

    def tearDown(self):
        # Runs after each test method, even if it failed
        self.orders = None

    def test_total(self):
        assert sum(o["amount"] for o in self.orders) == 350.0

    def test_count(self):
        assert len(self.orders) == 2
```

Because `setUp` runs fresh before each test, one test cannot contaminate another by modifying shared data.

---

## Testing with pytest

`pytest` is a separate package, installed with `pip install pytest`, and it takes a simpler approach. Tests can be plain functions, and plain `assert` statements are used directly, since `pytest` rewrites them internally to produce detailed failure messages.

```python
def add(a, b):
    return a + b

def test_add_positive_numbers():
    assert add(2, 3) == 5

def test_add_negative_numbers():
    assert add(-2, -3) == -5

def test_add_zero():
    assert add(0, 5) == 5
```

This file is run from the command line with:

```text
pytest test_add.py
```

## Test Discovery

`pytest` finds tests automatically by following naming conventions. Understanding these avoids the common frustration of tests silently not running:

- Files must be named `test_*.py` or `*_test.py`
- Functions must start with `test_`
- Classes must start with `Test` and must not define an `__init__` method

Running `pytest` with no arguments searches the current directory and everything below it. A test that does not follow these conventions is simply not collected, and no error is reported, which is why a test that appears to be ignored is usually a naming problem.

## Running Specific Tests

Running the whole suite every time is slow once it grows. Tests can be selected in several ways:

```text
pytest test_add.py                    # one file
pytest test_add.py::test_add_zero     # one specific test
pytest -k "zero or negative"          # tests whose names match an expression
pytest -v                             # verbose, lists each test by name
pytest -x                             # stop at the first failure
pytest --tb=short                     # shorter failure tracebacks
```

The `-k` option is particularly useful during development, since it runs only the tests relevant to whatever is being worked on.

---

## Comparing unittest and pytest

| | unittest | pytest |
|---|---|---|
| Installation | Built in, no setup needed | Requires `pip install pytest` |
| Test structure | Class based, inherits `TestCase` | Plain functions |
| Assertions | Special methods like `assertEqual` | Plain `assert` statements |
| Output detail | Adequate | Generally more detailed and readable |
| Common usage | Legacy codebases, some enterprise standards | Most modern Python projects |

Both frameworks are capable of testing the same code. `unittest` is worth knowing because it requires no installation and appears in many existing codebases. `pytest` is worth knowing because it has become the more common choice for new projects, largely due to its simpler syntax and more readable output.

---

## Reading Test Output

When tests pass, both frameworks report a short success summary, for example a line of dots in `unittest` or a line reading `3 passed` in `pytest`. When a test fails, the output includes:

- Which test failed, by name.
- The exact assertion that did not hold.
- The expected value versus the actual value.

Reading this output correctly is the fastest way to fix a broken test, since it usually points directly at the mismatch without needing to add print statements or re-run the code manually.