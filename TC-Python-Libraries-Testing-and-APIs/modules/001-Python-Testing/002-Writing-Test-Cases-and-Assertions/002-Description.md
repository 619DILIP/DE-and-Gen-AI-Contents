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