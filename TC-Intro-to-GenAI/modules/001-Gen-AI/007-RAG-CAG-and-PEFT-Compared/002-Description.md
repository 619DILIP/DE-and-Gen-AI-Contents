## The Problem All of These Solve

A language model knows what was in its training data, and nothing else. That creates two practical gaps:

- **It does not know your data.** Internal documentation, a product catalogue, last quarter's figures, a private codebase. None of it was in the training data.
- **Its knowledge has a fixed cutoff.** Anything that happened or changed after training finished is invisible to it.

Asking a model about either produces one of two unhelpful outcomes: an admission that it does not know, or a confident fabrication of the kind covered in the hallucinations material.

Four approaches address this, and they are frequently confused with one another because they solve overlapping problems by very different means.

---

## Approach 1: Putting Context in the Prompt

The simplest option is including the relevant information directly in the prompt, as covered in the prompt engineering material.

```text
Here is our refund policy:
[policy text pasted here]

Using only the policy above, answer: can a customer return an
opened item after 45 days?
```

This works well and should be the first thing tried. It stops working when the information is too large to fit in the prompt, or when nobody knows in advance which part of a large body of information is relevant to a given question.

---

## Approach 2: Retrieval Augmented Generation (RAG)

RAG automates the step of finding the relevant information and inserting it into the prompt.

The insight is that a question asked in plain language rarely shares exact words with the document that answers it. Someone asking "how long do I have to send something back" needs the refund policy, which may never use the word "back". Keyword search handles this badly. RAG uses **embeddings** instead.

An embedding is a numeric representation of a piece of text, produced by a model, positioned so that text with similar meaning ends up numerically close together. "How long do I have to send something back" and "returns must be initiated within 30 days" land near each other despite sharing almost no words.

The process has two phases.

**Preparation, done once and repeated when the source data changes:**

```text
Documents
   -> split into chunks
   -> each chunk converted to an embedding
   -> embeddings stored in a vector store
```

**At query time, for every question:**

```text
User question
   -> converted to an embedding
   -> vector store finds the closest matching chunks
   -> those chunks inserted into the prompt alongside the question
   -> model generates an answer grounded in them
```

A **vector store** is a database built to answer the question "which stored items are closest to this one", quickly, across a very large number of items.

The properties worth remembering:

- Knowledge can be updated by changing the source documents. No retraining is involved.
- Answers can cite which chunks were used, which makes verification possible.
- The model itself is never modified.
- Retrieval quality determines answer quality. If the wrong chunks are retrieved, the model answers confidently from the wrong material.

---

## Approach 3: Cache Augmented Generation (CAG)

CAG takes a different route. Rather than retrieving a small relevant subset for each question, it loads the entire body of knowledge into the model's context up front, and reuses the model's internal processing of that content across many questions.

This became practical as context windows grew large enough to hold a substantial document set at once. Where RAG asks "which parts are relevant", CAG says "all of it is available, every time".

```text
RAG:  question -> find relevant chunks -> answer from those
CAG:  entire knowledge set preloaded -> question -> answer from all of it
```

The trade offs are fairly direct:

- **No retrieval step**, so no risk of retrieving the wrong chunks, and lower latency per question.
- **Simpler**, with no vector store, no chunking strategy, and no embedding model to maintain.
- **Bounded by the context window.** It only works while the whole knowledge set fits. RAG has no such ceiling.
- **Cost scales with the size of the loaded content**, not with the small relevant portion.

CAG suits a knowledge set that is modest, stable, and queried often. A product manual, an internal policy handbook, an API reference. RAG suits large or rapidly changing collections.

---

## Approach 4: Fine Tuning and PEFT

The first three approaches leave the model untouched and change what it is given. Fine tuning changes the model itself, by continuing its training on a smaller, specific dataset.

Full fine tuning updates every parameter in the model. For a large model that means enormous compute requirements and a full copy of the model stored per task, which is impractical for most organizations.

**Parameter Efficient Fine Tuning (PEFT)** is a family of techniques that get most of the benefit by updating only a small fraction of the parameters, leaving the rest frozen.

The most widely used is **LoRA**, Low Rank Adaptation. Rather than modifying the original weights, it trains a small set of additional weights alongside them. The result is a small file, often a few megabytes against a base model of many gigabytes, which is loaded on top of the unchanged base model.

This has a practical consequence worth noticing: several different LoRA adapters can be trained for different tasks and swapped against the same base model, rather than storing a separately fine tuned copy for each.

The critical point, and the one most often misunderstood: **fine tuning teaches behavior, not facts.** It is effective for adopting a consistent tone, producing a specific output format reliably, or following domain conventions. It is a poor and expensive way to give a model access to information, because the information becomes fixed at training time, cannot be cited, and requires retraining to update. That is what RAG and CAG are for.

---

## Comparing the Four

| | Prompt context | RAG | CAG | PEFT |
|---|---|---|---|---|
| What changes | The prompt | The prompt, automatically | The prompt, preloaded | The model |
| Solves | Small, known context | Access to large or changing knowledge | Access to a modest, stable knowledge set | Consistent behavior, tone, format |
| Updating knowledge | Edit the prompt | Update the source documents | Reload the content | Retrain |
| Can cite sources | Yes | Yes | Partly | No |
| Setup effort | None | Moderate, needs a vector store | Low | High, needs a training dataset |
| Main limit | Context size | Retrieval quality | Context size | Cost, and does not handle facts |

---

## Choosing Between Them

A workable order of consideration:

1. **Can the needed information simply go in the prompt?** If yes, do that. It is free and immediate.
2. **Is the knowledge set modest and stable enough to preload?** If yes, CAG avoids the machinery of retrieval.
3. **Is the knowledge set large, or does it change often?** If yes, RAG.
4. **Is the problem actually about behavior rather than knowledge?** If the model has the information but keeps expressing it in the wrong tone, format, or style, and prompting has not fixed it reliably, then PEFT.

These are not mutually exclusive. A common production arrangement uses RAG for knowledge and a fine tuned model for tone and format, because they address genuinely different problems.