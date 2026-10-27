<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Identify common categories of LLM use cases within software development.
- Explain how LLMs are used for code generation, explanation, and review.
- Describe how LLMs can assist with documentation and testing.
- Recognize which development tasks benefit most from LLM assistance.
- Explain why human oversight remains necessary across these use cases.

</details>

<details><summary>Description</summary>

## A Practical Categorization

Large language models are applied across several distinct categories of software development work. Understanding these categories helps clarify where these tools tend to add the most value, building directly on the earlier module covering how LLMs generate text based on learned patterns.

---

## Code Generation

LLMs can generate code from a natural language description, ranging from a single function to a larger block of boilerplate structure. This is most effective for common, well understood patterns, such as a standard function to parse a specific file format or a typical API endpoint structure, where the model has likely seen many similar examples during training.

```text
Prompt: "Write a Python function that reads a CSV file and returns
the number of rows that contain a missing value in any column."
```

For highly specific or unusual business logic that depends on context the model does not have, generated code typically needs more correction and review, consistent with the prompt engineering practices covered earlier regarding providing sufficient context.

---

## Code Explanation

LLMs are also used to explain existing code in plain language, which is particularly useful when working with unfamiliar code, a legacy codebase, or a language a developer is less experienced with. Pasting a function and asking for a plain language explanation of what it does can speed up the process of understanding code significantly faster than reading through it line by line unaided, especially for dense or unfamiliar syntax.

---

## Code Review Assistance

LLMs can review a code change and surface potential issues, such as unused variables, inconsistent naming, or common patterns known to cause bugs. This does not replace a human code review, particularly for judgment calls about design and architecture, but it can catch some categories of issues quickly and consistently, freeing up human reviewers to focus more attention on the aspects of a review that require genuine judgment.

---

## Documentation

Writing and maintaining documentation is a task many developers find tedious, which makes it a strong fit for LLM assistance. Given a function's code, a model can draft an initial description of its parameters, return value, and behavior, which a developer then reviews and refines rather than writing entirely from scratch.

---

## Test Generation

Building on the Python testing content covered earlier in this course, LLMs can suggest test cases for a given function, including edge cases a developer might not have immediately thought of. This connects the testing concepts covered earlier, such as typical values, edge cases, and invalid input, directly to a practical, AI assisted workflow: a developer can ask a model to suggest test cases for a function and then evaluate which of those suggestions are actually relevant and correct.

---

## Where Human Oversight Remains Necessary

Across every use case above, the same underlying limitation applies: the model does not verify correctness, it generates fluent, plausible output based on learned patterns, as covered in the earlier module on how LLMs work and the module on hallucinations. This means generated code still needs to be tested, generated explanations still need to be checked against the actual code, and generated documentation still needs to be verified for accuracy, rather than being trusted automatically simply because it reads clearly and confidently.

</details>

<details><summary>Real World Application</summary>

## A Typical Assisted Workflow

A developer working on a new feature might use an LLM to generate an initial draft of a function based on a description, ask the model to explain a related piece of unfamiliar legacy code they need to integrate with, then ask for suggested test cases covering that new function's edge cases. At each step, the developer reviews and adjusts the output rather than accepting it directly, treating the model as a fast, capable collaborator whose output still requires the same verification any other collaborator's work would receive.

</details>

<details><summary>Implementation</summary>

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

</details>

<details><summary>Summary</summary>

In this module, we learned:

- LLMs are commonly used across code generation, explanation, review assistance, documentation, and test generation.
- Code generation works best for common, well understood patterns rather than highly specific business logic.
- Code explanation and review assistance speed up understanding and catch some categories of issues quickly.
- Test generation connects directly to earlier testing fundamentals, suggesting cases a developer can evaluate and refine.
- Human oversight remains necessary across every use case, since these tools generate plausible output without verifying correctness.

With use cases covered, the next module looks at fine tuning, one of the ways a model can be adapted to a specific task or domain.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
