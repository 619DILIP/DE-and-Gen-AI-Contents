<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Define hallucination in the context of language models.
- Explain why hallucinations occur, connecting back to how these models generate text.
- Identify common situations where hallucinations are more likely.
- Describe practical strategies for reducing and catching hallucinations.
- Explain why verification remains the user's responsibility.

</details>

<details><summary>Description</summary>

## What Is a Hallucination?

In the context of language models, a hallucination refers to output that is presented confidently and fluently, but that is factually incorrect, fabricated, or not actually supported by any real source. This might be an invented statistic, a citation to a source that does not exist, or a confident but wrong answer to a factual question.

The term is somewhat misleading if taken too literally, since the model is not perceiving something falsely the way the word suggests in a human context. It is a useful shorthand for describing output that sounds plausible but is not accurate.

---

## Why Hallucinations Happen

Understanding why hallucinations occur connects directly back to how language models work, covered earlier. A model generates text by predicting the most statistically likely next token, based on patterns learned from its training data. It does not have a built in mechanism for verifying whether a specific fact is true. It is optimized to produce fluent, plausible sounding text, not to check that text against a ground truth.

This means a model can produce a confident, well written, and completely fabricated answer with the exact same fluency and tone as a correct one. Fluency and factual accuracy are simply not the same thing, and nothing about a hallucinated response tends to look obviously different from an accurate one on the surface.

---

## Situations Where Hallucinations Are More Likely

Hallucinations tend to occur more often when:

- A question asks about very specific, obscure, or recent information that may be underrepresented in the model's training data.
- A prompt asks the model to cite specific sources, statistics, or quotes, which the model may generate in a plausible sounding format even without a real source behind them.
- A question has no correct answer, or the correct answer is genuinely unknown, but the model still attempts to provide a confident sounding response rather than acknowledging uncertainty.

---

## Reducing and Catching Hallucinations

A few practical strategies help reduce the risk and impact of hallucinations:

- **Ask for sources, then verify them independently**: If a model provides a citation or statistic, treat it as a starting point to check, not as a confirmed fact.
- **Cross check important factual claims**: For anything that matters, particularly numbers, dates, or specific claims, verify against an independent, trusted source before relying on it.
- **Be more skeptical of very specific or obscure claims**: The more specific and unusual a claim is, the more valuable it is to verify, since specificity can make a fabricated answer feel more credible without actually making it more accurate.
- **Ask the model to indicate uncertainty**: Prompting a model to explicitly state when it is unsure, rather than always answering confidently, can sometimes surface useful signals, though this is not a guaranteed solution.

---

## Verification Remains the User's Responsibility

None of the strategies above eliminate hallucinations entirely, since they are a structural characteristic of how these models generate text, not a rare bug that will simply be fixed with enough refinement. The practical implication is that verifying important information ultimately remains the responsibility of the person using the tool, particularly for any output that will be shared, published, or used to make a real decision.

</details>

<details><summary>Real World Application</summary>

## Hallucinations in a Development Context

A developer asking an AI tool to explain what a specific library function does might receive an answer that sounds entirely plausible but describes behavior the function does not actually have, particularly for less common or more recently released libraries. Treating that explanation as a starting point, then checking it against the library's actual documentation before relying on it in real code, is the practical habit that prevents a fluent but incorrect answer from turning into a real bug.

</details>

<details><summary>Implementation</summary>

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

</details>

<details><summary>Summary</summary>

In this module, we learned:

- A hallucination is confident, fluent output from a language model that is factually incorrect or fabricated.
- Hallucinations occur because models are optimized for fluent text generation, not fact verification.
- They are more likely with obscure information, requests for specific citations, or questions with no clear answer.
- Practical strategies include verifying sources independently and being more skeptical of highly specific claims.
- Verifying important information ultimately remains the responsibility of the person using the tool.

Understanding this limitation sets up the next module, which looks more broadly at responsible use of generative AI.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
