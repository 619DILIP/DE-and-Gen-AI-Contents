## Installing the Extension

1. Open the extensions panel in the code editor.
2. Search for the Copilot extension and install it.
3. Sign in with an account that has an active subscription.
4. Confirm the status indicator shows the extension is active.
5. Open a code file and begin typing to see suggestions appear.

## Giving Copilot Useful Context

```python
# Weak context: generic name, no description
def f(x):
    pass
```

```python
# Strong context: descriptive name, clear comment, type hints
def calculate_monthly_average(daily_values: list[float]) -> float:
    """Return the average of daily values, or 0.0 if the list is empty."""
    pass
```

The second version gives the tool enough context to suggest a relevant implementation.

## Common Keyboard Actions

```text
Tab            Accept the current suggestion
Escape         Dismiss the suggestion
Alt + ]        View the next alternative suggestion
Alt + [        View the previous alternative suggestion
```

Exact bindings vary by editor and can be reconfigured in settings.

## Evaluating a Suggestion

```python
# Suggested implementation
def calculate_monthly_average(daily_values):
    return sum(daily_values) / len(daily_values)
```

Reviewing against the docstring reveals a problem: an empty list raises `ZeroDivisionError` rather than returning 0.0 as specified.

```python
# Corrected after review
def calculate_monthly_average(daily_values):
    if not daily_values:
        return 0.0
    return sum(daily_values) / len(daily_values)
```

## Steps to Follow

1. Write a descriptive function name and docstring first.
2. Let the suggestion appear, then read it fully before accepting.
3. Check the suggestion against edge cases stated in the docstring.
4. Correct anything the suggestion missed.
5. Write tests confirming the corrected behavior.
