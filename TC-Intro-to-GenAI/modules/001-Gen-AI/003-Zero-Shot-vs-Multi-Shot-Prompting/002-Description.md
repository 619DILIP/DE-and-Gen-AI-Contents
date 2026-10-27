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
