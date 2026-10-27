<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Explain what AI pair programming means and how it differs from traditional pair programming.
- Describe how GitHub Copilot generates suggestions as a developer writes code.
- Apply effective habits for working with Copilot, including writing clear comments and function signatures.
- Evaluate a Copilot suggestion before accepting it.
- Recognize the limitations of AI pair programming tools.

</details>

<details><summary>Description</summary>

## What Is AI Pair Programming?

Traditional pair programming involves two developers working together at one workstation, one writing code while the other reviews and suggests improvements in real time. AI pair programming applies a similar concept, but the second participant is an AI tool that suggests code as a developer writes, based on the current file's context.

GitHub Copilot is one of the most widely used tools in this category, integrating directly into a code editor and offering suggestions ranging from completing the current line to generating an entire function based on a comment or a function signature.

---

## How Copilot Generates Suggestions

Copilot is built on the same underlying large language model concepts covered earlier in this section. As a developer types, Copilot uses the surrounding code, including comments, variable names, and existing functions in the file, as context to predict what code is likely to come next, applying the same next token prediction mechanism covered in the module on how LLMs work, specifically trained and tuned for code.

```python
# Function to check if a number is a prime number
def is_prime(n):
    # Copilot is likely to suggest an implementation here,
    # based on the comment and function signature above
```

Because Copilot's suggestions are generated from surrounding context, the quality of that context directly affects the quality of its suggestions, which is why clear naming and comments matter more when working with these tools, not less.

---

## Effective Habits for Working with Copilot

- **Write clear, descriptive comments before a function**: A comment that clearly states what a function should do gives Copilot the context needed to generate a relevant suggestion, similar to how a clear prompt improves output in the prompt engineering modules covered earlier.
- **Use descriptive function and variable names**: Names like `calculate_average` and `total_price` give Copilot more useful context than generic names like `func1` or `x`.
- **Break large problems into smaller functions**: Copilot tends to generate more accurate suggestions for smaller, well defined pieces of logic than for one large, complex function attempting to do many things at once.
- **Review suggestions actively, rather than accepting by default**: Treat every suggestion as a draft to evaluate, not an automatic accept, consistent with the responsible usage practices covered earlier in this section.

---

## Evaluating a Suggestion Before Accepting It

Before accepting a Copilot suggestion, it helps to ask:

- Does this suggestion actually solve the problem correctly, including edge cases?
- Does it follow the existing code's style and conventions?
- Does it introduce a dependency or approach that was not already part of the project?
- Would this pass the tests already written for this function, or the tests that should be written for it, connecting directly back to the testing skills covered earlier in this course?

A suggestion that looks reasonable at a glance can still contain a subtle bug, particularly for edge cases the surrounding context did not make obvious to the model, consistent with the hallucination and code generation risks covered earlier in this section.

---

## Limitations

Copilot and similar tools work from the context available in the current file and, to a limited extent, other open files in a project. They generally do not have full knowledge of an entire large codebase, external documentation specific to an organization, or business requirements that were never written down anywhere in the code itself. Suggestions involving highly specific business logic, or logic that depends on context outside the currently visible code, tend to require significantly more correction than suggestions for common, self contained patterns.

</details>

<details><summary>Real World Application</summary>

## Copilot in a Real Coding Session

A developer implementing a data validation function might write a clear comment describing exactly what should be validated, then let Copilot suggest an initial implementation. Rather than accepting it immediately, the developer checks the suggestion against a mental list of edge cases, such as empty input or unexpected data types, adjusts anything missing, and then writes or reviews the accompanying test cases before considering the function complete. This workflow treats Copilot as a fast way to produce a first draft, while keeping the review and verification responsibility firmly with the developer.

</details>

<details><summary>Implementation</summary>

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

</details>

<details><summary>Summary</summary>

In this module, we learned:

- AI pair programming applies the collaborative review concept of traditional pair programming, with an AI tool suggesting code in real time.
- Copilot generates suggestions based on the surrounding code context, using the same underlying mechanism as other language models.
- Clear comments, descriptive names, and smaller functions all improve the quality of Copilot's suggestions.
- Suggestions should be actively evaluated for correctness, style, and edge cases before being accepted.
- Copilot's suggestions are limited by the context visible to it and may require more correction for highly specific business logic.

With AI pair programming covered, the final module of this section looks in more depth at using these tools to analyze and improve existing code.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
