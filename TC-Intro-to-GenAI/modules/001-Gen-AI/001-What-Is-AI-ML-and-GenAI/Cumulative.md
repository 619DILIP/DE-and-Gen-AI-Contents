<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Define artificial intelligence, machine learning, and generative AI.
- Explain how these three terms relate to each other.
- Describe the general idea behind how a machine learning model learns from data.
- Explain what makes generative AI distinct from earlier forms of machine learning.
- Identify common examples of generative AI in current use.

</details>

<details><summary>Description</summary>

## Three Related but Distinct Terms

Artificial intelligence, machine learning, and generative AI are often used interchangeably in casual conversation, but they describe increasingly specific concepts, each nested within the one before it.

```text
Artificial Intelligence
    └── Machine Learning
            └── Generative AI
```

---

## Artificial Intelligence

Artificial intelligence, or AI, is the broadest of the three terms. It refers generally to systems that perform tasks which would normally require human intelligence, such as recognizing images, understanding language, or making decisions based on data. AI as a field of study dates back decades and includes many approaches beyond the ones covered in this module, some of which do not involve learning from data at all, but instead rely on explicitly programmed rules.

---

## Machine Learning

Machine learning, or ML, is a specific approach to building AI systems, where instead of explicitly programming every rule a system should follow, the system is trained on data and learns patterns from that data on its own.

For example, rather than writing explicit rules to detect spam email, a machine learning model is shown thousands of examples of emails already labeled as spam or not spam, and it learns which patterns, such as certain words or sender characteristics, are associated with each label. Once trained, it can apply what it learned to new, unseen emails.

Machine learning includes many different techniques and model types, and it underlies a large portion of modern AI applications, from recommendation systems to voice assistants.

---

## Generative AI

Generative AI, or GenAI, is a more recent and specific category of machine learning, focused on models that generate new content, text, images, audio, or code, rather than simply classifying or predicting a value from existing data.

A traditional machine learning model trained on emails might predict whether a new email is spam. A generative AI model, by contrast, could be trained to write a new email from scratch, given a description of what it should contain.

The most widely known form of generative AI today is the large language model, or LLM, which is trained on vast amounts of text and learns to generate coherent, contextually relevant text in response to a prompt. LLMs are covered in more depth in a later module.

---

## What Makes GenAI Different

Earlier forms of machine learning were largely built to make a specific, narrow prediction or classification: is this transaction fraudulent, will this customer cancel their subscription, what number does this handwritten digit represent. Generative AI models are trained to produce open ended output, which makes them useful across a much broader range of tasks without needing to be built and trained separately for each one.

This flexibility is also what makes generative AI both powerful and, as covered in later modules on responsible use, more difficult to fully predict and control compared to narrower, task specific machine learning models.

---

## Common Examples of GenAI Today

- Text generation tools that draft emails, summaries, or articles based on a prompt.
- Code generation and pair programming tools, covered later in this section, that suggest or write code based on context.
- Image generation tools that create original images from a text description.
- Conversational assistants that hold open ended, natural language conversations.

</details>

<details><summary>Real World Application</summary>

## GenAI in Software Development

Software development is one of the areas where generative AI has had the most immediate, practical impact. Developers now commonly use AI powered tools that suggest code as they type, generate boilerplate code from a description, or explain unfamiliar code in plain language. This does not replace the underlying programming skills covered throughout this curriculum. It changes how those skills are applied day to day, which is why understanding the fundamentals of AI, machine learning, and generative AI is directly relevant to a modern development career, not just a general interest topic.

</details>

<details><summary>Implementation</summary>

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

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Artificial intelligence is the broad field of building systems that perform tasks requiring human like intelligence.
- Machine learning is a specific AI approach where systems learn patterns from data rather than following explicitly programmed rules.
- Generative AI is a category of machine learning focused on generating new content, most notably through large language models.
- Generative AI's flexibility, producing open ended output, distinguishes it from narrower, task specific machine learning models.
- Generative AI is already widely used in software development, content creation, and conversational tools.

With these foundational terms defined, the next module moves into prompt engineering, the practical skill of communicating effectively with these models.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
