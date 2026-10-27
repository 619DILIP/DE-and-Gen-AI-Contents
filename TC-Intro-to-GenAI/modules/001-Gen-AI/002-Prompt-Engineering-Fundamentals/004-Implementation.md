## Building a Prompt Step by Step

Starting from a vague request and improving it.

```text
Version 1 (vague):
"Summarize this."

Version 2 (adds instruction):
"Summarize this article."

Version 3 (adds format):
"Summarize this article in three bullet points."

Version 4 (adds audience and constraint):
"Summarize this article in three bullet points for a technical
audience. Focus on the findings rather than the methodology,
and keep each bullet under twenty words."
```

## A Reusable Prompt Template

```python
def build_prompt(task, context, output_format, constraints):
    return f"""Task: {task}

Context:
{context}

Output format:
{output_format}

Constraints:
{constraints}
"""

prompt = build_prompt(
    task="Write release notes for a software update",
    context="Version 2.4 fixes a login timeout bug and adds CSV export",
    output_format="A short paragraph followed by a bulleted list of changes",
    constraints="Keep it under 150 words, no marketing language"
)
print(prompt)
```

## Iterating on a Response

```text
First prompt:
"Explain what this function does."

Follow up after reviewing the response:
"That explanation is too detailed. Rewrite it as two sentences
aimed at someone unfamiliar with this codebase."
```

## Steps to Follow

1. State the task directly rather than implying it.
2. Include the context the model cannot know on its own.
3. Specify the output format explicitly.
4. Add constraints on length, tone, or content.
5. Review the response and refine the prompt rather than starting over.
