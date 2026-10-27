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