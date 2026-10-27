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
