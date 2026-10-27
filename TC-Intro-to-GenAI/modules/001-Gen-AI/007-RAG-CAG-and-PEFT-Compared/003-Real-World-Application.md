## An Internal Support Assistant

A company wants an assistant that answers employee questions from internal documentation covering HR policies, IT procedures, and engineering runbooks.

Fine tuning on that documentation would be the wrong instinct, even though it sounds like the most thorough option. The documentation changes regularly, retraining on every change is impractical, the model could not cite which policy an answer came from, and the result would be prone to confidently blending details from unrelated policies.

RAG fits the shape of the problem. Documents are chunked and embedded once. A question retrieves the few most relevant chunks, the model answers from them, and the answer cites which documents were used so the employee can verify it. Updating a policy means updating the document.

If the same company later found the assistant's answers technically correct but consistently too informal for HR communications, that is a behavior problem rather than a knowledge problem, and PEFT would be the appropriate tool, applied alongside the RAG setup rather than instead of it.