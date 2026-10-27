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