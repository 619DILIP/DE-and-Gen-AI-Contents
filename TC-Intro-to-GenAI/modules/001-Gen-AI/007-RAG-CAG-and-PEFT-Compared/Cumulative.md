<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Explain the knowledge problem that these techniques exist to solve.
- Describe how Retrieval Augmented Generation works and what an embedding and a vector store do.
- Describe Cache Augmented Generation and how it differs from retrieval.
- Explain what Parameter Efficient Fine Tuning changes compared with full fine tuning.
- Compare the four approaches across cost, freshness, and the kind of problem each solves.
- Select an appropriate approach for a given scenario.

</details>

<details><summary>Description</summary>

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

</details>

<details><summary>Real World Application</summary>

## An Internal Support Assistant

A company wants an assistant that answers employee questions from internal documentation covering HR policies, IT procedures, and engineering runbooks.

Fine tuning on that documentation would be the wrong instinct, even though it sounds like the most thorough option. The documentation changes regularly, retraining on every change is impractical, the model could not cite which policy an answer came from, and the result would be prone to confidently blending details from unrelated policies.

RAG fits the shape of the problem. Documents are chunked and embedded once. A question retrieves the few most relevant chunks, the model answers from them, and the answer cites which documents were used so the employee can verify it. Updating a policy means updating the document.

If the same company later found the assistant's answers technically correct but consistently too informal for HR communications, that is a behavior problem rather than a knowledge problem, and PEFT would be the appropriate tool, applied alongside the RAG setup rather than instead of it.

</details>

<details><summary>Implementation</summary>

## A Minimal RAG Pipeline

The mechanics, without any particular framework, to show what each stage does.

```python
# 1. Prepare: chunk the documents
def chunk_text(text, size=500, overlap=50):
    chunks = []
    start = 0
    while start < len(text):
        chunks.append(text[start:start + size])
        start += size - overlap
    return chunks
```

The overlap matters. A sentence split across a boundary is lost to retrieval unless chunks share some text.

```python
# 2. Prepare: embed each chunk and store it
store = []

def index_document(text, source_name, embed_fn):
    for i, chunk in enumerate(chunk_text(text)):
        store.append({
            "source": source_name,
            "chunk_id": i,
            "text": chunk,
            "embedding": embed_fn(chunk),
        })
```

```python
# 3. Query: find the closest chunks
def cosine_similarity(a, b):
    dot = sum(x * y for x, y in zip(a, b))
    na = sum(x * x for x in a) ** 0.5
    nb = sum(y * y for y in b) ** 0.5
    return dot / (na * nb) if na and nb else 0.0

def retrieve(question, embed_fn, top_k=3):
    q = embed_fn(question)
    scored = [(cosine_similarity(q, item["embedding"]), item) for item in store]
    scored.sort(key=lambda pair: pair[0], reverse=True)
    return [item for _, item in scored[:top_k]]
```

```python
# 4. Query: build a grounded prompt
def build_prompt(question, chunks):
    context = "\n\n".join(
        f"[{c['source']} #{c['chunk_id']}]\n{c['text']}" for c in chunks
    )
    return f"""Answer the question using only the context below.
If the context does not contain the answer, say so rather than guessing.
Cite the source labels you used.

Context:
{context}

Question: {question}
"""
```

The instruction to say so rather than guessing is doing real work. Without it, a model given irrelevant context will often answer anyway, from its training data, while appearing to answer from the provided material.

In production, the hand written similarity search is replaced by a purpose built vector store, which is far faster at scale, but the stages are the same.

---

## The CAG Equivalent

```python
def build_cag_prompt(question, knowledge_documents):
    everything = "\n\n---\n\n".join(knowledge_documents)
    return f"""You have been given the complete reference material below.
Answer the question using only this material.

{everything}

Question: {question}
"""
```

No chunking, no embeddings, no retrieval. The constraint is that `everything` must fit within the context window, and that its size is paid for on every question.

---

## Checking Retrieval Before Blaming the Model

When a RAG system answers badly, the cause is usually retrieval rather than generation. Inspecting what was retrieved is the fastest diagnosis.

```python
question = "how long do I have to return an item"
chunks = retrieve(question, embed_fn)

for c in chunks:
    print(f"--- {c['source']} #{c['chunk_id']}")
    print(c["text"][:200])
```

If the correct passage is not in the retrieved set, no amount of prompt adjustment will fix the answer. The usual causes are chunks that are too large and dilute the relevant content, too small and lose its context, or a source document that never covered the topic in the first place.

---

## Evaluating a RAG System

Two things need measuring separately, because they fail for different reasons.

```python
def evaluate(test_cases, embed_fn):
    retrieval_hits = 0
    for question, expected_source in test_cases:
        retrieved = retrieve(question, embed_fn)
        if any(c["source"] == expected_source for c in retrieved):
            retrieval_hits += 1
    print(f"Retrieval accuracy: {retrieval_hits}/{len(test_cases)}")
```

Retrieval accuracy asks whether the right material was found. Answer quality asks whether the model used it correctly. A system can score well on one and badly on the other, and the fix differs entirely depending on which.

---

## Steps to Follow

1. Establish whether the problem is about knowledge or about behavior. This determines everything that follows.
2. For knowledge, try putting the context directly in the prompt first.
3. If the knowledge set is modest and stable, preload it (CAG) before building retrieval machinery.
4. If it is large or changes often, build RAG: chunk with overlap, embed, store, retrieve, and ground the prompt.
5. Instruct the model to answer only from the provided context and to say when it cannot.
6. Measure retrieval accuracy separately from answer quality.
7. Reach for PEFT only when the problem is behavioral and prompting has genuinely failed to fix it.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- A model knows only its training data, which creates gaps around private information and anything after its cutoff.
- Putting context directly in the prompt is the simplest approach and should be tried first.
- RAG converts text to embeddings, stores them in a vector store, retrieves the most relevant chunks per question, and grounds the answer in them.
- CAG preloads an entire knowledge set into context rather than retrieving per question, trading scale for simplicity.
- PEFT, most commonly LoRA, fine tunes a small fraction of parameters rather than all of them.
- Fine tuning teaches behavior, not facts; knowledge problems belong to RAG or CAG.
- The approaches combine, and production systems frequently use RAG for knowledge alongside a fine tuned model for tone.

With the ways of supplying a model with knowledge covered, the next module turns to hallucinations, a key limitation to understand when relying on any model's output.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>