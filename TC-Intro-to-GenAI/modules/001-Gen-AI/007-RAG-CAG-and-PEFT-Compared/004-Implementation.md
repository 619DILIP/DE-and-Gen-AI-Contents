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