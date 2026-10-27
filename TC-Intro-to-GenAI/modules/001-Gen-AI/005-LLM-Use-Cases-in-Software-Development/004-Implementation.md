## Generating Code from a Description

```text
Prompt:
"Write a Python function that takes a list of dictionaries and
returns only those where the 'status' key equals 'active'.
Include a docstring and handle the case where the key is missing."
```

```python
def filter_active(records):
    """Return records whose status is 'active'.

    Records missing a 'status' key are excluded.
    """
    return [r for r in records if r.get("status") == "active"]
```

## Requesting an Explanation of Existing Code

```text
Prompt:
"Explain what this function does in plain language, including
what happens with an empty input."

[paste the function here]
```

## Generating Test Cases

```text
Prompt:
"Suggest pytest test cases for this function, covering typical
input, edge cases, and invalid input."

[paste the function here]
```

```python
def test_filter_active_typical():
    records = [{"status": "active"}, {"status": "inactive"}]
    assert len(filter_active(records)) == 1

def test_filter_active_empty():
    assert filter_active([]) == []

def test_filter_active_missing_key():
    records = [{"name": "x"}, {"status": "active"}]
    assert len(filter_active(records)) == 1
```

## Reviewing Generated Output

```text
Before accepting generated code:

1. Does it handle empty or missing input?
2. Does it match the project's existing style?
3. Does it introduce any new dependency?
4. Do existing tests still pass?
5. Has it been read line by line, not just skimmed?
```

## Steps to Follow

1. Describe the task clearly, including edge cases that matter.
2. Provide relevant surrounding context in the prompt.
3. Read the generated output carefully rather than accepting it directly.
4. Write or request tests covering the generated behavior.
5. Run the tests before committing the code.
