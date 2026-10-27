## The Core Idea: Predicting What Comes Next

At the most basic level, a large language model is trained to do one thing extremely well: given some text, predict what text is most likely to come next. This sounds simple, but doing it well across nearly any topic, style, or format requires learning an enormous number of patterns about how language, facts, and reasoning tend to fit together.

When a model generates a longer response, it is repeatedly applying this same prediction, one small piece at a time, using everything generated so far as context for predicting the next piece.

```text
Prompt: "The capital of France is"
Model predicts the most likely next word: "Paris"

Prompt: "The capital of France is Paris"
Model predicts the most likely next word: "."
```

This process repeats until the model produces a complete response.

---

## Tokens, Not Just Words

Models do not process text one whole word at a time. Text is broken into smaller pieces called tokens, which can be whole words, parts of words, or punctuation, depending on how common that piece of text is. A common word might be a single token, while a rare or unusual word might be split into several tokens.

```text
"unbelievable" might be broken into tokens like: "un", "believ", "able"
```

This matters practically because the length of a prompt and a model's response are usually measured and limited in tokens, not in words or characters, which is relevant later when working with prompt engineering and considering cost or length limits.

---

## Training Data

A large language model learns its patterns by being trained on an enormous amount of text, often drawn from a broad cross section of publicly available writing, covering countless topics, styles, and languages. During training, the model is repeatedly shown text and adjusts itself to get better at predicting the next token, across billions of examples.

The scale of this training data is part of what allows a model to generate coherent, relevant text across such a wide range of topics. It is also directly connected to some of the model's limitations, covered in a later module, since the model can only reflect patterns present in the data it was trained on, and that data has a fixed cutoff point in time.

---

## Pattern Matching, Not True Understanding

It is worth being precise about what is actually happening inside a language model. The model is not reasoning about the world the way a person does, and it does not have beliefs, intentions, or genuine understanding of the content it produces. It is recognizing and reproducing extremely sophisticated statistical patterns in language, learned from its training data.

This distinction matters practically. A model can produce text that sounds confident and fluent while still being factually incorrect, because fluency and factual accuracy are not the same thing, and the model's core skill is fluency, built on pattern prediction rather than verified fact checking. This connects directly to the topic of hallucinations, covered later in this section.

---

## From Prediction to Conversation

Modern LLMs are further refined after their initial training, through a process that adjusts them to follow instructions and hold a conversational back and forth, rather than only continuing text in a raw, unstructured way. This is part of what makes tools like conversational AI assistants feel like they are responding directly to a request, rather than simply continuing a block of text, even though the underlying mechanism is still fundamentally the same next token prediction process described above.
