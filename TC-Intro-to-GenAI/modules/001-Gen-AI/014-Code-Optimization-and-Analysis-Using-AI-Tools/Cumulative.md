<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Distinguish AI assisted code analysis from traditional static analysis.
- Use AI tools to identify performance problems and reason about algorithmic complexity.
- Apply AI assistance to refactoring while preserving behavior.
- Use AI tools to understand unfamiliar or legacy code.
- Recognize what these tools cannot determine about running code.
- Follow a measure, change, verify workflow rather than optimizing on suggestion alone.

</details>

<details><summary>Description</summary>

## Two Different Kinds of Analysis

Developers have had automated code analysis for a long time. Linters and static analysis tools parse code against a fixed set of rules and report violations: an unused variable, a missing return, a line over the length limit.

Those tools are precise and deterministic. The same code produces the same findings every time, and a reported violation is genuinely a violation. What they cannot do is reason about intent. A linter will not tell you that a function is slow because it queries the database inside a loop, because no rule describes that.

AI assisted analysis works differently. It reasons over the code in context and can identify problems that no rule anticipated. The trade off is the one that applies throughout this section: it is not deterministic, and it can be confidently wrong.

| | Static analysis | AI assisted analysis |
|---|---|---|
| Based on | Fixed rules | Learned patterns |
| Consistency | Identical every run | Varies between runs |
| Finds | Rule violations | Patterns, intent problems, design issues |
| Reliability | A finding is a real finding | A finding may be wrong |
| Explains reasoning | Rarely | Usually |

They are complementary. Static analysis is the floor, catching mechanical problems reliably. AI analysis reaches problems that need judgment, at the cost of needing judgment applied to its output.

---

## Performance and Complexity Analysis

One of the more useful applications is reasoning about how code behaves as its input grows.

```python
def find_duplicates(records):
    duplicates = []
    for i in range(len(records)):
        for j in range(len(records)):
            if i != j and records[i]["id"] == records[j]["id"]:
                if records[i] not in duplicates:
                    duplicates.append(records[i])
    return duplicates
```

Asked to analyze this for performance, a capable tool will identify several distinct problems: the nested loop makes it quadratic in the number of records, the membership test against a list adds another linear scan inside that, and every pair is compared twice. On a hundred records this is invisible. On a hundred thousand it is the difference between instant and unusable.

```python
def find_duplicates(records):
    seen = set()
    duplicates = {}
    for record in records:
        rid = record["id"]
        if rid in seen and rid not in duplicates:
            duplicates[rid] = record
        seen.add(rid)
    return list(duplicates.values())
```

The value here is not that the tool wrote the replacement. It is that it named the specific reason the original was slow, which is transferable knowledge. A developer who understands why the nested loop was the problem recognizes the pattern next time without asking.

---

## Refactoring

Refactoring means changing the structure of code without changing what it does. AI tools are well suited to the mechanical parts: extracting a repeated block into a function, replacing a long conditional chain with a lookup, simplifying nested logic, improving names.

The essential discipline is that behavior must not change. That means tests come first.

```text
1. Confirm tests exist and pass
2. Request the refactoring
3. Review the suggestion against what the code is supposed to do
4. Apply it
5. Run the tests again
6. If they fail, the refactoring changed behavior. Revert rather than adjust the tests.
```

Step six matters more than it appears. When a test fails after a refactoring, the instinct is sometimes to update the test. That converts a refactoring into a behavior change without anyone deciding to make one. The testing material covered earlier is what makes this workflow possible at all; without tests, a refactoring is a hope rather than a verified change.

---

## Understanding Unfamiliar Code

Explaining existing code is often the highest value use of these tools day to day, particularly for a legacy codebase or a language a developer knows less well.

Useful requests go beyond asking what code does:

- Explain this function in plain language, including what happens with empty input.
- What assumptions does this code make about its inputs?
- What edge cases does this not handle?
- Why might this have been written this way rather than the obvious approach?

That last question is worth asking. Unusual looking code sometimes exists for a reason that is no longer visible, such as a workaround for a bug in a dependency. A tool cannot know the actual history, but it can suggest plausible reasons that prompt the right investigation rather than an immediate rewrite.

---

## Security and Correctness Review

AI tools can surface common vulnerability patterns: string concatenation into SQL queries, unvalidated input reaching a filesystem path, secrets committed in code, missing error handling around external calls.

This is genuinely useful as an extra pair of eyes, and equally genuinely not a security audit. A clean result means nothing was recognized, not that nothing is there. The security practices covered earlier in this section still apply, and generated code carries exactly the same risk as any other code.

---

## What These Tools Cannot Determine

The limits follow from the fact that the tool reads code but does not run it.

- **It has no measurements.** It cannot know which function actually consumes the runtime in your system, only which looks expensive. The two frequently differ.
- **It does not know your data.** A nested loop over a list that never exceeds ten items is fine. Without knowing the realistic size, a tool cannot judge whether a theoretical problem is a real one.
- **It sees limited context.** A change that looks safe in one file may break a caller elsewhere that the tool never saw.
- **It cannot confirm behavior is preserved.** Only tests can do that.
- **It may be confidently wrong.** A suggested optimization can be slower, or subtly incorrect, while being explained persuasively.

The last two are why the workflow below ends with verification rather than with applying a suggestion.

---

## Measure, Change, Verify

The oldest rule in performance work applies unchanged: do not optimize what you have not measured.

```text
1. Measure, and find where the time is actually spent
2. Ask for analysis of that specific code
3. Evaluate the suggestion rather than accepting it
4. Apply one change
5. Run the tests, confirming behavior is unchanged
6. Measure again, confirming it is actually faster
7. Keep it only if both hold
```

Steps five and six are the ones that get skipped, and skipping them is how a codebase accumulates changes that were believed to be improvements without anyone confirming they were.

</details>

<details><summary>Real World Application</summary>

## Investigating a Slow Report

A nightly report that used to finish in minutes now takes over an hour, and the data volume has grown considerably since it was written.

Asking a tool to make the report faster without more information invites guesses at whatever looks worst. Profiling first shows that almost all the time sits in one function, which turns out to query the database once per row rather than once for the whole set. That specific function is then the thing to hand over for analysis, and the suggestion, batching the lookups into a single query, addresses the actual cause.

The report's existing tests confirm the output is unchanged, and a second timing run confirms the improvement is real. Every other candidate the tool might have flagged in a broader review would have been a distraction, because none of them accounted for meaningful runtime.

</details>

<details><summary>Implementation</summary>

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

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Static analysis applies fixed rules reliably; AI assisted analysis reasons over context but can be wrong.
- AI tools are effective at identifying algorithmic complexity problems and explaining why code is slow.
- Refactoring with AI assistance depends on tests, which are what confirm behavior was preserved.
- Explaining unfamiliar or legacy code is one of the highest value everyday uses.
- Security review assistance is an extra pair of eyes, not an audit; a clean result proves nothing.
- These tools cannot measure runtime, know realistic data sizes, or see the full codebase.
- The measure, change, verify workflow is what separates an actual improvement from a believed one.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>