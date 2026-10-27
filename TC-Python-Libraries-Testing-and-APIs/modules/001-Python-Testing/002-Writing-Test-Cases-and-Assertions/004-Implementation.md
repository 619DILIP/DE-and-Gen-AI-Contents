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