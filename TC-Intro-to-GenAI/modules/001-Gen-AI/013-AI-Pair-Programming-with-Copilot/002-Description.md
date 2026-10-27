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
