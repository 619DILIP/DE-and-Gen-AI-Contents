<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Define zero shot prompting and identify when it is sufficient.
- Define few shot, or multi shot, prompting and explain how it differs from zero shot.
- Construct a multi shot prompt using consistent, well chosen examples.
- Explain the tradeoffs between the two approaches, including prompt length and consistency.
- Choose an appropriate approach for a given task.

</details>

<details><summary>Description</summary>

## Zero Shot Prompting

Zero shot prompting means asking a model to complete a task by describing it directly, without providing any worked examples of what the desired output should look like. The model relies entirely on its general training to interpret the instruction and produce a reasonable response.

```text
Zero shot prompt:
"Classify the sentiment of this review as positive, negative, or
neutral: 'The delivery was late but the product itself works great.'"
```

Zero shot prompting works well for tasks that are common and well understood, where the model has likely seen many similar examples during training, such as basic classification, summarization, or straightforward rewriting tasks.

---

## Few Shot, or Multi Shot, Prompting

Few shot prompting, also called multi shot prompting, means including one or more worked examples directly in the prompt before asking the model to complete a new, similar case. These examples demonstrate exactly the pattern or format expected.

```text
Multi shot prompt:

Example 1:
Review: "Fast shipping and the item matched the description perfectly."
Sentiment: Positive

Example 2:
Review: "The item arrived damaged and customer service never responded."
Sentiment: Negative

Example 3:
Review: "It's fine, does what it's supposed to, nothing special."
Sentiment: Neutral

Now classify this review:
Review: "The delivery was late but the product itself works great."
Sentiment:
```

By showing several labeled examples first, the prompt communicates the exact expected format and the specific criteria being used to judge sentiment, which reduces ambiguity compared to relying on the instruction alone.

---

## Why Examples Help

Providing examples is especially useful when:

- The task involves a specific, less common format that the model might not default to on its own.
- The criteria for a correct answer are somewhat subjective or specific to a particular use case, where showing several examples defines the boundary more precisely than a written description could.
- Consistency across many outputs matters, such as when classifying a large batch of similar items and needing every result to follow the exact same labeling convention.

---

## Tradeoffs Between the Two Approaches

| | Zero Shot | Multi Shot |
|---|---|---|
| Prompt length | Shorter | Longer, since it includes examples |
| Setup effort | Minimal | Requires selecting good, representative examples |
| Consistency | Can vary more across responses | Generally more consistent, since the pattern is explicitly shown |
| Best suited for | Common, well understood tasks | Specific, nuanced, or format sensitive tasks |

A longer, multi shot prompt also consumes more tokens, which can matter for cost and for staying within a model's context length, so the added consistency needs to be worth that additional length for the task at hand.

---

## Choosing Which Approach to Use

A reasonable default is to start with a zero shot prompt, since it requires the least effort to write. If the resulting output is inconsistent, misses the intended format, or misunderstands the specific criteria being applied, adding a small number of well chosen examples through multi shot prompting is usually the most direct way to correct that, rather than trying to describe the desired behavior in increasingly detailed written instructions alone.

</details>

<details><summary>Real World Application</summary>

## Classifying Support Tickets

A team using a language model to automatically categorize incoming customer support tickets into categories such as billing, technical issue, or feature request might start with a zero shot prompt describing the categories. If the model's categorization turns out inconsistent, particularly for tickets that could reasonably fit more than one category, the team can switch to a multi shot prompt that includes a handful of real, previously categorized tickets as examples. This grounds the model's decision making in the team's actual categorization conventions, rather than a generic interpretation of the category names alone.

</details>

<details><summary>Implementation</summary>

## Implementing a Zero Shot Prompt

```python
def zero_shot_classify(review):
    return f"""Classify the sentiment of this review as
positive, negative, or neutral.

Review: {review}
Sentiment:"""

print(zero_shot_classify("The delivery was late but the product works great."))
```

## Implementing a Multi Shot Prompt

```python
EXAMPLES = [
    ("Fast shipping and the item matched the description.", "Positive"),
    ("Arrived damaged and support never responded.", "Negative"),
    ("It's fine, does what it's supposed to.", "Neutral")
]

def multi_shot_classify(review):
    example_text = ""
    for text, label in EXAMPLES:
        example_text += f"Review: {text}\nSentiment: {label}\n\n"

    return f"""Classify the sentiment of each review.

{example_text}Review: {review}
Sentiment:"""

print(multi_shot_classify("The delivery was late but the product works great."))
```

## Choosing Good Examples

```python
# Weak example set: all the same category
weak = [
    ("Great product", "Positive"),
    ("Love it", "Positive"),
    ("Excellent", "Positive")
]

# Strong example set: covers each category and includes
# a mixed case that clarifies the boundary
strong = [
    ("Great product, fast delivery", "Positive"),
    ("Broke after one day", "Negative"),
    ("Works fine, nothing remarkable", "Neutral"),
    ("Product is good but shipping was slow", "Positive")
]
```

## Steps to Follow

1. Start with a zero shot prompt describing the task.
2. Review the output for consistency and format accuracy.
3. If results vary, select examples covering each expected category.
4. Include at least one boundary case that clarifies ambiguous situations.
5. Keep the example count small enough to stay within token limits.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Zero shot prompting asks a model to complete a task from instructions alone, without examples.
- Few shot, or multi shot, prompting includes worked examples in the prompt to demonstrate the expected pattern.
- Multi shot prompting generally improves consistency and format accuracy at the cost of a longer prompt.
- Zero shot prompting is well suited to common, well understood tasks.
- A reasonable approach is to start with zero shot prompting and add examples only if the results need more consistency.

With prompting techniques covered, the next module looks more closely at how large language models actually work beneath the surface.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
