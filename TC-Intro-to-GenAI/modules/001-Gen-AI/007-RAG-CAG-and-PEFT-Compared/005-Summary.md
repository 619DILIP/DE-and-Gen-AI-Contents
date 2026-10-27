In this module, we learned:

- A model knows only its training data, which creates gaps around private information and anything after its cutoff.
- Putting context directly in the prompt is the simplest approach and should be tried first.
- RAG converts text to embeddings, stores them in a vector store, retrieves the most relevant chunks per question, and grounds the answer in them.
- CAG preloads an entire knowledge set into context rather than retrieving per question, trading scale for simplicity.
- PEFT, most commonly LoRA, fine tunes a small fraction of parameters rather than all of them.
- Fine tuning teaches behavior, not facts; knowledge problems belong to RAG or CAG.
- The approaches combine, and production systems frequently use RAG for knowledge alongside a fine tuned model for tone.

With the ways of supplying a model with knowledge covered, the next module turns to hallucinations, a key limitation to understand when relying on any model's output.