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
