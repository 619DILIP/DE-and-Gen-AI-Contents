<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Define fine tuning and explain how it differs from prompting.
- Describe the general process of fine tuning a pre trained model.
- Identify scenarios where fine tuning provides an advantage over prompting alone.
- Explain the cost and effort tradeoffs of fine tuning compared to prompt engineering.
- Recognize that fine tuning and prompting are not mutually exclusive approaches.

</details>

<details><summary>Description</summary>

## What Is Fine Tuning?

Fine tuning is the process of taking a model that has already been trained on a broad, general dataset and further training it on a smaller, more specific dataset, so it becomes better suited to a particular task, style, or domain. This is different from prompting, covered in earlier modules, where the underlying model itself is never changed, only the input given to it at the time of use.

```text
Pre trained General Model  →  Additional Training on Specific Data  →  Fine Tuned Model
```

---

## Why Not Just Train a Model From Scratch?

Training a large language model from nothing requires an enormous amount of data and computing power, well beyond what is practical for most organizations. Fine tuning avoids this by starting from a model that already understands language broadly, and only adjusting it using a much smaller, targeted dataset relevant to the specific task at hand. This makes fine tuning dramatically more efficient than training a new model from scratch, while still allowing meaningful customization.

---

## When Fine Tuning Helps

Fine tuning is particularly useful when:

- A task requires a very specific tone, style, or format that is difficult to consistently achieve through prompting alone, even with the multi shot techniques covered earlier.
- An organization has a large volume of domain specific data, such as internal support tickets or specialized technical documentation, and wants a model to reliably reflect that specific domain's language and conventions.
- The same type of request will be made repeatedly at scale, where consistently getting the right format without needing to repeat lengthy instructions or examples in every single prompt provides a meaningful efficiency benefit.

---

## Fine Tuning vs Prompting

| | Prompting | Fine Tuning |
|---|---|---|
| What changes | Only the input given to the model | The model's own internal parameters |
| Effort required | Low, can be adjusted instantly | Higher, requires a prepared dataset and a training process |
| Cost | Generally lower, pay per use | Generally higher, due to the training process itself |
| Best suited for | Most everyday tasks, especially ones that vary | Narrow, repeated, high volume tasks needing very specific behavior |
| Flexibility | Easy to adjust on the fly | Requires retraining to make significant changes |

---

## Prompting and Fine Tuning Are Not Mutually Exclusive

In practice, prompting and fine tuning are often used together rather than as competing choices. A fine tuned model still receives prompts at the time it is used, and good prompt engineering practices still improve its output, even though the underlying model has already been customized through fine tuning. Most organizations start with prompt engineering, since it requires no additional training process, and only invest in fine tuning once they have a clear, repeated, well defined need that prompting alone cannot reliably satisfy.

</details>

<details><summary>Real World Application</summary>

## Fine Tuning for a Specialized Support Assistant

A company handling a very high volume of highly specific technical support questions might fine tune a model on thousands of its own past support conversations and internal documentation. This can produce a model that responds using the company's exact terminology and support conventions more consistently than prompting a general model with instructions and a handful of examples each time. The company would still write careful prompts when using this fine tuned model, but it would need less repeated context and fewer examples in each individual prompt, since much of that specific knowledge has already been incorporated into the model itself through the fine tuning process.

</details>

<details><summary>Implementation</summary>

## Preparing a Fine Tuning Dataset

Fine tuning data is typically formatted as input and output pairs.

```python
import json

training_data = [
    {
        "input": "Customer reports the export button is greyed out",
        "output": "Category: UI Bug\nPriority: Medium\nTeam: Frontend"
    },
    {
        "input": "Invoice charged twice for the same月 period",
        "output": "Category: Billing\nPriority: High\nTeam: Payments"
    }
]

with open("training_data.jsonl", "w") as f:
    for item in training_data:
        f.write(json.dumps(item) + "\n")
```

## Deciding Whether Fine Tuning Is Warranted

```text
Checklist before investing in fine tuning:

1. Has prompt engineering been tried thoroughly first?
2. Is the task narrow and repeated at high volume?
3. Are there at least several hundred quality examples available?
4. Is the desired behavior stable, not likely to change soon?
5. Does the cost of training justify the improvement expected?

If several answers are no, prompt engineering is usually
the better investment.
```

## Evaluating a Fine Tuned Model

```python
def evaluate(model_fn, test_cases):
    correct = 0
    for input_text, expected in test_cases:
        result = model_fn(input_text)
        if result.strip() == expected.strip():
            correct += 1
    accuracy = correct / len(test_cases)
    print(f"Accuracy: {accuracy:.2%}")
    return accuracy
```

A held out set of test cases, not used during training, is needed to measure whether fine tuning actually improved results.

## Steps to Follow

1. Exhaust prompt engineering approaches first.
2. Collect a dataset of quality input and output pairs.
3. Hold back a portion of that data for evaluation.
4. Run the fine tuning process on the training portion.
5. Measure accuracy against the held out data before adopting the model.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Fine tuning further trains a pre trained model on a smaller, specific dataset to customize its behavior.
- Fine tuning is more efficient than training a model from scratch, while still allowing meaningful customization.
- It is most valuable for narrow, high volume, or highly specific tasks that prompting alone struggles to satisfy consistently.
- Fine tuning requires more upfront effort and cost compared to prompting.
- Prompting and fine tuning are complementary techniques, often used together rather than as alternatives.

With fine tuning covered, the next module compares it against the other common approaches for supplying a model with knowledge it was not trained on.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
