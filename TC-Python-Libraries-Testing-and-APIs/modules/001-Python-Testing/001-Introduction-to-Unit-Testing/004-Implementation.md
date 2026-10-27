## Setting Up a Test File

A common convention is to keep test code in a separate file, named after the file it tests.

```text
project/
    calculator.py
    test_calculator.py
```

## Writing a First Test

```python
# calculator.py
def add(a, b):
    return a + b
```

```python
# test_calculator.py
from calculator import add

def test_add():
    assert add(2, 3) == 5

test_add()
print("Test passed")
```

## Steps to Follow

1. Identify a single function to test.
2. Create a test file alongside the code file.
3. Import the function into the test file.
4. Write one assertion covering the expected behavior.
5. Run the test file and confirm it completes without an error.

## Checking That a Test Actually Works

A test that never fails is not proving anything. Temporarily break the function to confirm the test catches it.

```python
def add(a, b):
    return a - b   # deliberately wrong

# Running the test now raises AssertionError, confirming
# the test is actually checking the behavior.
```

Restore the correct implementation once confirmed.