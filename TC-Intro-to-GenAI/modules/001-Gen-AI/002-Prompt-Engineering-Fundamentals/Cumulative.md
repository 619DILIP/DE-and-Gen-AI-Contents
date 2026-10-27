<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Define prompt engineering and explain why it matters.
- Identify the components of an effective prompt.
- Apply techniques such as providing context, specifying format, and giving examples.
- Explain the concept of iterative prompting.
- Recognize common prompting mistakes and how to avoid them.

</details>

<details><summary>Description</summary>

## What Is Prompt Engineering?

Prompt engineering is the practice of writing input, called a prompt, in a way that reliably produces useful output from a language model. Since a model generates its response based entirely on the text it is given, the way a request is phrased has a direct and often significant effect on the quality, relevance, and format of the result.

This is not a matter of finding secret phrasing tricks. It follows the same logic as communicating clearly with a person: a vague, ambiguous request tends to produce a vague, generic response, while a clear, specific request tends to produce a clear, specific response.

---

## Components of an Effective Prompt

A strong prompt typically includes some combination of the following:

- **Clear instruction**: State directly what is being asked for, rather than implying it.
- **Context**: Provide relevant background information the model needs to give a useful answer.
- **Format specification**: Describe how the output should be structured, such as a bulleted list, a specific length, or a particular tone.
- **Constraints**: Specify what should be avoided or included, such as excluding certain terms or requiring a certain style.

```text
Weak prompt:
"Write something about our new product."

Stronger prompt:
"Write a two paragraph announcement for a new project management
tool aimed at small business owners. Keep the tone professional
but approachable, and mention that it integrates with existing
calendar apps."
```

The second prompt gives the model enough context and constraints to produce something close to what is actually needed on the first attempt, rather than something generic that requires significant rewriting.

---

## Providing Examples

When a specific format or style is important, providing an example directly in the prompt is often more effective than describing that format in words alone.

```text
Prompt:
"Rewrite the following bug report in this format:

Format example:
Title: Short summary
Steps to Reproduce: numbered list
Expected Result: one sentence
Actual Result: one sentence

Bug report to rewrite: [original messy bug report text]"
```

Showing the model exactly what the output should look like, rather than only describing it abstractly, tends to produce more consistent, usable results.

---

## Iterative Prompting

Prompt engineering is rarely a single attempt that gets everything right immediately. A more realistic and effective approach treats the interaction as a conversation: review the model's response, identify what is missing or incorrect, and refine the next prompt based on that. This might mean adding missing context, correcting a misunderstanding, or asking the model to adjust the tone or length of its previous response.

```text
Initial prompt: "Summarize this article in one paragraph."
Follow up prompt: "Make that summary more concise and remove the
introductory sentence, since I only need the key findings."
```

This iterative back and forth is a normal, expected part of using these tools effectively, not a sign that the first prompt was written incorrectly.

---

## Common Prompting Mistakes

- **Being too vague**: Leaving out important context the model has no way of knowing, then being surprised the response misses the mark.
- **Assuming the model remembers unstated context**: A model only knows what has been included in the current conversation. It does not automatically know details about a specific project or codebase unless they are provided directly.
- **Not specifying format**: Leaving the response format completely open when a specific format, such as a table or a numbered list, is actually needed.
- **Overloading a single prompt**: Asking for too many distinct things at once, which can lead to some parts of the request being addressed weakly or skipped entirely.

</details>

<details><summary>Real World Application</summary>

## Prompting in a Development Workflow

A developer asking an AI tool to help refactor a function benefits significantly from including relevant context directly in the prompt: the function's current code, what it is supposed to do, and any specific constraint, such as maintaining backward compatibility with existing calls to that function. A vague request like "make this code better" leaves the model guessing at priorities that the developer already knows but has not communicated. Learning to communicate that context clearly and concisely is a practical skill that directly affects how useful these tools are in day to day development work.

</details>

<details><summary>Implementation</summary>

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

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Prompt engineering is the practice of writing input that reliably produces useful output from a language model.
- Effective prompts typically include clear instructions, relevant context, format specifications, and constraints.
- Providing a concrete example of the desired output often improves consistency more than description alone.
- Prompting is commonly iterative, refining a request based on the model's previous response.
- Common mistakes include vagueness, assuming unstated context, and overloading a single prompt with too many requests.

With these fundamentals covered, the next module looks specifically at zero shot and multi shot prompting, two related but distinct approaches to structuring a prompt.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
