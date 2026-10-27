<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Write a test case that checks a specific piece of behavior.
- Use Python's `assert` statement correctly.
- Identify what to check when writing a test case, including typical and edge case inputs.
- Explain what an assertion failure means and how to read it.
- Organize multiple related test cases for the same function.

</details>

<details><summary>Description</summary>

## What Is a Test Case?

A test case is a single, specific check: given this input, the function should produce this output. A function usually needs more than one test case, since one input is rarely enough to prove that the function works correctly across every situation it might encounter.

For example, a function that checks whether a number is positive needs at least three test cases:

- A positive number, which should return `True`.
- A negative number, which should return `False`.
- Zero, which is a boundary case worth checking explicitly.

```python
def is_positive(number):
    return number > 0

assert is_positive(5) == True
assert is_positive(-3) == False
assert is_positive(0) == False
```

---

## The Assert Statement

Python's built in `assert` statement is the foundation of writing test cases. The syntax is:

```python
assert condition, "optional message"
```

If `condition` evaluates to `True`, nothing happens and execution continues. If it evaluates to `False`, Python raises an `AssertionError`. The optional message is shown alongside the error, which makes it easier to understand what went wrong without having to read the test code itself.

```python
def add(a, b):
    return a + b

result = add(2, 2)
assert result == 4, f"Expected 4 but got {result}"
```

If `add` had a bug and returned 5, the assertion would fail and print: `Expected 4 but got 5`. This message is what makes debugging a failing test faster than debugging a silent wrong answer somewhere deep in a program.

---

## Deciding What to Test

A common mistake when starting out is writing only one test case per function, usually the most obvious one. A stronger set of test cases covers:

- **Typical input**: the kind of value the function is expected to receive most of the time.
- **Edge cases**: values at the boundary of what is valid, such as zero, an empty list, or the largest allowed value.
- **Invalid or unexpected input**: values that should be rejected or handled in a specific way, such as a negative number where only positive numbers make sense.

```python
def calculate_average(numbers):
    if len(numbers) == 0:
        return 0
    return sum(numbers) / len(numbers)

assert calculate_average([2, 4, 6]) == 4        # typical case
assert calculate_average([]) == 0               # edge case: empty list
assert calculate_average([5]) == 5              # edge case: single item
```

Without the empty list case, a bug in how the function handles an empty input could go unnoticed until it caused a real failure in production.

---

## Organizing Multiple Test Cases

As the number of test cases grows, it helps to group them under a single function per unit being tested, so the test file reads clearly and can be run as one unit.

```python
def test_calculate_average():
    assert calculate_average([2, 4, 6]) == 4
    assert calculate_average([]) == 0
    assert calculate_average([5]) == 5

test_calculate_average()
print("All tests passed")
```

This is a manual version of what testing frameworks automate. Frameworks such as `unittest` and `pytest`, covered next, remove the need to call test functions manually and to print confirmation messages by hand.

</details>

<details><summary>Real World Application</summary>

## Writing Tests Alongside Features

In practice, developers write test cases for a function around the same time they write the function itself, rather than as an afterthought. When a bug is reported in existing code, the standard first step is to write a new test case that reproduces the bug, confirm that it fails, then fix the code until the test passes. That new test case then stays in the codebase permanently, so the same bug cannot silently return later without being caught.

</details>

<details><summary>Implementation</summary>

## Building a Full Set of Test Cases

```python
def apply_discount(price, percent):
    if percent < 0 or percent > 100:
        raise ValueError("Percent must be between 0 and 100")
    return price - (price * percent / 100)
```

```python
def test_apply_discount():
    # typical case
    assert apply_discount(100, 10) == 90

    # edge case: no discount
    assert apply_discount(100, 0) == 100

    # edge case: full discount
    assert apply_discount(100, 100) == 0

    # invalid input
    try:
        apply_discount(100, 150)
        assert False, "Expected ValueError for percent above 100"
    except ValueError:
        pass

test_apply_discount()
print("All tests passed")
```

## Steps to Follow

1. Write down what the function should do for a normal input.
2. Identify the boundaries of valid input, such as zero or a maximum value.
3. Identify what should happen for invalid input.
4. Write one assertion per behavior identified.
5. Add a clear failure message to any assertion whose purpose is not obvious.

## Using Assertion Messages

```python
result = apply_discount(200, 25)
assert result == 150, f"Expected 150 for 25 percent off 200, got {result}"
```

</details>

<details><summary>Summary</summary>

In this module, we learned:

- A test case is a single, specific input and expected output check.
- The `assert` statement is the core building block of a test case in Python.
- Good test coverage includes typical values, edge cases, and invalid input.
- Assertion failures produce clear error messages that speed up debugging.
- Related test cases can be grouped into a single test function for organization.

With this foundation, the next step is learning how Python's dedicated testing tools, `unittest` and `pytest`, automate running and reporting on test cases like these.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
