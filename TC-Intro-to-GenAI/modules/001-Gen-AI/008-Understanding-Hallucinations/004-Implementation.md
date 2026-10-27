## Building Verification Into a Workflow

```python
def review_generated_claims(response_text):
    checklist = {
        "contains_statistics": False,
        "contains_citations": False,
        "contains_dates": False,
        "requires_verification": False
    }

    indicators = ["%", "percent", "study", "according to", "research"]
    for indicator in indicators:
        if indicator in response_text.lower():
            checklist["requires_verification"] = True

    return checklist
```

Flagging responses containing statistics or citations highlights exactly which parts need independent checking.

## Prompting to Reduce Fabrication

```text
Weaker prompt:
"What are the key statistics on this topic?"

Stronger prompt:
"Explain this topic. If you are not confident about a specific
figure or source, say so explicitly rather than providing an
estimate. Do not invent citations."
```

## Grounding a Response in Provided Material

Supplying source material and restricting the model to it reduces fabrication.

```python
def grounded_prompt(question, source_document):
    return f"""Answer the question using only the document below.
If the document does not contain the answer, say
"The document does not contain this information."

Document:
{source_document}

Question: {question}
"""
```

## Steps to Follow

1. Identify which parts of a response contain factual claims.
2. Flag statistics, citations, dates, and specific figures for checking.
3. Verify each flagged claim against an independent, trusted source.
4. Where possible, supply source material and restrict the model to it.
5. Never publish or act on an unverified specific claim.
