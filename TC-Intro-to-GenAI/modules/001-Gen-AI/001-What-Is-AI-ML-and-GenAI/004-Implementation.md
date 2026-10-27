## Recognizing Which Category a Problem Falls Into

Given a problem, identifying the appropriate category guides which approach to consider.

```text
Problem: Sort emails into spam and not spam
Category: Machine Learning (classification)

Problem: Write a draft reply to an email
Category: Generative AI (text generation)

Problem: Apply a fixed set of business rules to route a ticket
Category: Traditional programming, no learning required
```

## A Simple Classification Example

A traditional machine learning task predicts a label from existing data.

```python
# Conceptual example of a classification task
training_examples = [
    ("win a free prize now", "spam"),
    ("meeting moved to 3pm", "not spam"),
    ("claim your reward today", "spam"),
    ("please review the attached report", "not spam")
]

# A model learns which patterns associate with which label,
# then predicts a label for new, unseen text.
```

## A Generative Task by Contrast

```text
Input:  "Write a short, polite reply declining a meeting invitation."
Output: New text produced by the model, not a label selected
        from a fixed set of options.
```

The key difference is that the output is generated content rather than a choice among predefined categories.

## Steps to Follow

1. State the problem in plain language.
2. Determine whether the output is a label, a number, or new content.
3. If the output is a label or number, consider traditional machine learning.
4. If the output is new content, consider generative AI.
5. If the rules are fixed and known, consider standard programming instead.
