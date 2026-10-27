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
