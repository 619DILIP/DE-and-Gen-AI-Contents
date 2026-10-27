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
