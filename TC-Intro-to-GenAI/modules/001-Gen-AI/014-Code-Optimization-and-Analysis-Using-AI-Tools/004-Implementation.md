## Measuring Before Asking

```python
import cProfile
import pstats

def run_report():
    generate_monthly_report("2024-06")

profiler = cProfile.Profile()
profiler.enable()
run_report()
profiler.disable()

stats = pstats.Stats(profiler)
stats.sort_stats("cumulative").print_stats(10)
```

The ten functions listed by cumulative time are where optimization effort belongs. Anything not on that list is not worth changing for performance reasons, however inefficient it looks.

For a quick comparison of two implementations:

```python
import timeit

original = timeit.timeit(lambda: find_duplicates_v1(sample), number=100)
revised  = timeit.timeit(lambda: find_duplicates_v2(sample), number=100)

print(f"original: {original:.4f}s")
print(f"revised:  {revised:.4f}s")
print(f"change:   {original / revised:.1f}x")
```

---

## Asking Well

Context determines the quality of the analysis. Compare:

```text
Weak:
"Make this faster."

Strong:
"This function is called once per request and receives a list of
roughly 50,000 order records. Profiling shows it accounts for 70
percent of request time. Analyze it for performance problems,
explain the cause of each, and note any trade off in readability
for the changes you suggest."
```

The second supplies the three things the tool cannot know on its own: realistic data size, where the time actually goes, and what matters besides speed.

---

## Verifying a Suggested Optimization

```python
import pytest

# Behavior first: same output for the same inputs
@pytest.mark.parametrize("records,expected_count", [
    ([], 0),
    ([{"id": 1}], 0),
    ([{"id": 1}, {"id": 1}], 1),
    ([{"id": 1}, {"id": 2}, {"id": 1}, {"id": 2}], 2),
])
def test_behavior_unchanged(records, expected_count):
    assert len(find_duplicates_v2(records)) == expected_count

# Then equivalence against the original across generated inputs
def test_matches_original():
    import random
    for _ in range(50):
        sample = [{"id": random.randint(1, 20)} for _ in range(100)]
        a = sorted(r["id"] for r in find_duplicates_v1(sample))
        b = sorted(r["id"] for r in find_duplicates_v2(sample))
        assert a == b
```

The second test is the more valuable of the two. Comparing the new implementation against the old across many random inputs catches divergence that a handful of hand written cases would miss, and it is cheap to write.

---

## A Refactoring Session

```python
# Before
def process(data, mode):
    if mode == "sum":
        total = 0
        for d in data:
            total += d["value"]
        return total
    elif mode == "avg":
        total = 0
        for d in data:
            total += d["value"]
        return total / len(data)
    elif mode == "max":
        m = data[0]["value"]
        for d in data:
            if d["value"] > m:
                m = d["value"]
        return m
```

```text
Request:
"Refactor this to remove the duplicated iteration and make adding a
new mode straightforward. Keep the existing function signature, since
callers depend on it. Note any behavior that changes, particularly
for empty input."
```

```python
# After
OPERATIONS = {
    "sum": lambda values: sum(values),
    "avg": lambda values: sum(values) / len(values),
    "max": lambda values: max(values),
}

def process(data, mode):
    if mode not in OPERATIONS:
        raise ValueError(f"Unknown mode: {mode}")
    values = [d["value"] for d in data]
    return OPERATIONS[mode](values)
```

Asking explicitly about empty input was worthwhile. The original raised `IndexError` for `max` and `ZeroDivisionError` for `avg`; the refactored version raises `ValueError` for `max`. That is a behavior change, and it needs a deliberate decision rather than being discovered by a caller later.

---

## Requesting a Security Review

```text
"Review this function for security issues, specifically injection
risks, unvalidated input, and anything sensitive being logged.
For each finding, explain the risk and show the fix."
```

```python
# Flagged: query built by string formatting
def get_orders(customer_id):
    query = f"SELECT * FROM orders WHERE customer_id = {customer_id}"
    return db.execute(query).fetchall()

# Fixed: parameterized
def get_orders(customer_id):
    query = "SELECT * FROM orders WHERE customer_id = %s"
    return db.execute(query, (customer_id,)).fetchall()
```

This is the same parameterization practice covered in the SQL and API material. The tool is useful for spotting where it was forgotten, not for teaching it.

---

## Steps to Follow

1. Profile first, and work only on what the measurements identify.
2. Supply realistic data sizes and the profiling result when asking for analysis.
3. Confirm tests exist before any refactoring, and never adjust them to make a refactoring pass.
4. Apply one change at a time so the effect of each is attributable.
5. Verify behavior with tests, including an equivalence check against the original.
6. Measure again, and keep the change only if it is genuinely faster.
7. Treat a clean security review as nothing recognized, not as nothing present.