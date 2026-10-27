<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Define what a unit test is and what it checks.
- Explain why testing is a standard part of professional software development.
- Distinguish unit testing from other forms of testing such as integration and manual testing.
- Identify what makes a function easy or difficult to test.
- Describe the general structure that most unit tests follow.

</details>

<details><summary>Description</summary>

## What Is a Unit?

In programming, a unit is the smallest piece of code that can be tested on its own. In Python, this is usually a single function or method. A unit test checks that one unit behaves correctly for a given input, independent of the rest of the program.

If a function is supposed to add two numbers and return the result, a unit test for that function calls it with known inputs and checks that the output matches what is expected.

---

## Why Test Code at All?

Code is written to behave in a certain way. As a program grows, it becomes harder to be sure that a change in one place has not broken something in another. Manually running a script and reading the output works for small programs, but it does not scale, and it leaves no record that the check ever happened.

Automated tests solve this by turning manual checking into repeatable code. Once written, a test can be run in seconds, as many times as needed, and it will report the same result every time given the same code.

Common reasons teams write tests:

- To catch bugs early, before they reach production.
- To confirm that a bug fix actually fixes the bug and stays fixed.
- To make it safe to change or refactor code, since the tests reveal if something breaks.
- To document expected behavior in a form that can be executed rather than just read.

---

## Unit Testing vs Other Kinds of Testing

Testing exists at several levels, and unit testing is only one of them.

- **Unit testing** checks a single function or method in isolation.
- **Integration testing** checks that multiple units work correctly together, such as a function that reads from a database and a function that formats the result.
- **Manual testing** is a person running the program and observing the behavior directly, without any automated check.

Unit tests are usually the fastest to run and the easiest to write, which is why they typically make up the largest portion of a project's test suite.

---

## What Makes Code Testable?

Some functions are naturally easy to test, and others are difficult. A function is easier to test when it:

- Takes clear inputs and returns a clear output.
- Does not depend on external systems such as a network call or a file on disk.
- Does the same thing every time it is given the same input.

A function that reads the current time, generates a random number, or depends on user input during execution is harder to test directly, because its result is not the same every time. Writing testable code is a skill that improves with practice, and it often leads to cleaner function design in general.

---

## The General Shape of a Unit Test

Most unit tests follow the same three-part pattern, sometimes referred to as Arrange, Act, Assert:

1. **Arrange**: set up the inputs and any values needed to run the function.
2. **Act**: call the function being tested.
3. **Assert**: check that the actual result matches the expected result.

```python
def add(a, b):
    return a + b

# Arrange
first_number = 2
second_number = 3
expected_result = 5

# Act
actual_result = add(first_number, second_number)

# Assert
assert actual_result == expected_result
```

If the assertion is true, the test passes silently. If it is false, Python raises an `AssertionError`, which signals that the code did not behave as expected.

</details>

<details><summary>Real World Application</summary>

## Testing in a Development Workflow

In most professional teams, code is not considered complete until it has tests. When a developer submits a change, an automated system typically runs the full test suite before that change is allowed to merge. If a test fails, the change is blocked until it is fixed.

This matters most on teams where many people work on the same codebase. A developer changing one part of an application cannot manually check every other part that might depend on it, but a test suite can check all of it in seconds. This is why unit testing is treated as a core skill rather than an optional add on, regardless of the language or framework a team uses.

</details>

<details><summary>Implementation</summary>

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

</details>

<details><summary>Summary</summary>

In this module, we learned:

- A unit is the smallest testable piece of code, usually a single function.
- Unit tests check that a unit produces the expected output for a given input.
- Automated tests are repeatable, fast, and reduce the reliance on manual checking.
- Unit testing is distinct from integration testing and manual testing.
- Testable functions have clear inputs, clear outputs, and predictable behavior.
- Most unit tests follow the Arrange, Act, Assert pattern.

Understanding what a unit test is and why it matters sets up the practical work of writing test cases and using Python's testing tools.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
