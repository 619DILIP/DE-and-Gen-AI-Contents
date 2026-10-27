# Cumulative for pytest

<details><summary>Learning Objectives</summary>

# Learning Objectives
After completing this module, associates should be able to:

- Explain what pytest is and why automated testing is important
- Create simple test functions using pytest conventions
- Run tests from the command line and interpret basic output
- Use common pytest features such as `assert`, `fixtures`, and `parametrize`
- Organize tests into files and directories that pytest can discover automatically

</details>

<details><summary>Description</summary>

# What is pytest?

**pytest** is a popular testing framework for Python that makes it easy to write and run automated tests.

Compared to Python’s built-in `unittest` module, pytest focuses on:

- **Simple, readable tests** using plain `assert` statements
- **Automatic test discovery** based on naming conventions
- **Helpful failure messages** when assertions fail
- **Powerful extensions** such as fixtures, parametrized tests, and plugins

pytest is widely used in both small scripts and large production systems. Learning it early helps you build the habit of testing your code as you write it.

</details>

<details><summary>Real World Application</summary>

# Real World Application for pytest

In real projects, pytest is used to:

- Verify that **core business logic** works as expected
- Guard against **regressions** when changing or refactoring code
- Automatically test **data pipelines**, **APIs**, and **libraries**
- Run a full test suite in **CI/CD pipelines** (e.g., GitHub Actions, Jenkins, GitLab)

Examples:

- A data engineering team uses pytest to check that a transformation function always returns the correct columns and data types.
- A web team uses pytest to validate that API endpoints return the right status codes and JSON payloads.
- A library author uses pytest to ensure that bug fixes do not break other parts of the package.

Automated tests provide confidence: when tests pass, you have evidence that critical parts of your application still behave correctly.

</details>

<details><summary>Implementation</summary>

# Implementation

## Installing pytest

If pytest is not already available in your environment, you can install it with:

```bash
pip install pytest
```

Once installed, the `pytest` command becomes available in your terminal.

---

## Writing Your First Test

pytest discovers tests based on **naming conventions**:

* Files should be named like `test_something.py` or `something_test.py`
* Test functions should start with `test_`

Example project structure:

```text
my_project/
       src/
           calculator.py
       tests/
           test_calculator.py
           test_utils.py
```

`calculator.py`:

```python
def add(a, b):
    return a + b
```

`test_calculator.py`:

```python
from calculator import add

def test_add_two_positive_numbers():
    result = add(2, 3)
    assert result == 5
```

To run the tests, navigate to the project folder and use:

```bash
pytest
```

pytest will:

* Discover `test_calculator.py`
* Run `test_add_two_positive_numbers`
* Report whether the test passed or failed

---

## Using Assertions

pytest uses **plain Python `assert` statements**:

```python
def test_basic_math():
    assert 1 + 1 == 2
    assert 3 * 3 == 9
```

If an assertion fails, pytest shows a **clear error message** explaining the difference:

```text
>       assert 1 + 1 == 3
E       assert 2 == 3
```

---

## Parametrized Tests

Sometimes you want to test the same function with multiple inputs and expected outputs. pytest provides `@pytest.mark.parametrize` for this:

```python
import pytest
from calculator import add

@pytest.mark.parametrize(
    "a, b, expected",
    [
        (1, 1, 2),
        (2, 3, 5),
        (-1, 1, 0),
    ],
)
def test_add_various_values(a, b, expected):
    assert add(a, b) == expected
```

This is cleaner than writing three separate test functions.

---

## Fixtures for Setup and Teardown

A **fixture** is a reusable piece of setup code that tests can depend on. Fixtures are defined with the `@pytest.fixture` decorator.

Example:

```python
import pytest

@pytest.fixture # Can change scope using @pytest.fixture(scope="module")
def sample_list():
    # This object is created before each test that uses sample_list
    return [1, 2, 3]

def test_list_length(sample_list):
    assert len(sample_list) == 3

def test_list_contents(sample_list):
    assert sample_list[0] == 1
    assert sample_list[-1] == 3
```

pytest automatically passes the `sample_list` fixture into any test that declares it as a parameter.

---

## Running and Selecting Tests

Common commands:

```bash
# Run all tests in the current directory and subdirectories
pytest

# Run tests in a specific file
pytest test_calculator.py

# Run a single test function in a file
pytest test_calculator.py::test_add_two_positive_numbers

# Show more detailed output
pytest -v
```

These options are useful when your project grows and you want to target specific tests.

</details>

<details><summary>Summary</summary>

# Summary

* **pytest** is a powerful, easy-to-use testing framework for Python.
* It uses **simple naming conventions** to discover test files and test functions.
* Tests are written with plain **`assert` statements**, and pytest provides detailed failure messages.
* Features like **parametrized tests** and **fixtures** help avoid repetition and keep tests organized.
* Tests are run from the command line using the `pytest` command, with options to select specific files or tests.
* Using pytest regularly helps catch bugs early and gives confidence when modifying or extending code.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>