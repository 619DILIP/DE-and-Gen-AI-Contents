<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Explain what responsible AI usage means in a practical sense.
- Identify the risk of over reliance on AI generated output.
- Describe considerations around data privacy when using AI tools.
- Explain the importance of disclosing AI assistance where relevant.
- Recognize the concept of bias in AI generated content.

</details>

<details><summary>Description</summary>

## What Responsible Usage Means in Practice

Responsible AI usage is not a single rule but a set of practical habits that account for the limitations covered in earlier modules, particularly the tendency toward hallucination, and apply sound judgment about when and how to rely on these tools. It is less about avoiding these tools and more about using them with an accurate understanding of what they are actually good at and where they need oversight.

---

## The Risk of Over Reliance

One of the most common practical risks is over reliance: accepting AI generated output without applying the same judgment and review that would be applied to work from any other source. This risk grows specifically because these tools produce fluent, confident sounding output regardless of whether that output is correct, which can make it easy to skip the verification step that would normally happen with a less polished, less confident sounding source.

A useful habit is treating AI generated output the way a careful professional would treat a first draft from any source: a strong starting point, worth building on, but not automatically the final word.

---

## Data Privacy Considerations

Many AI tools, particularly ones accessed over the internet, process the text a user provides on external servers. This raises real considerations around what kind of information should or should not be included in a prompt:

- Sensitive personal information, such as customer data, should generally not be pasted directly into a general purpose AI tool unless that tool has been specifically approved and configured for that kind of data.
- Confidential business information, proprietary code, or trade secrets carry similar risk, since it may leave an organization's control once submitted to an external system.

Most organizations working with AI tools establish specific policies about what kinds of information are and are not appropriate to include in a prompt, and following those policies is a basic part of responsible usage.

---

## Disclosure

In many professional and academic contexts, there is an expectation to disclose when AI assistance was used to produce a piece of work, similar to how a source would be cited. This is not universal, and expectations vary by organization, publication, or academic institution, but checking and following the relevant disclosure expectations for a given context is part of using these tools responsibly rather than presenting AI generated work as entirely one's own without acknowledgment where that acknowledgment is expected.

---

## Bias in AI Generated Content

Because language models learn patterns from large amounts of existing text, they can also learn and reproduce biases present in that text, whether related to gender, culture, or other characteristics. This is not necessarily intentional or obvious, and it can appear subtly, for example in the kinds of examples a model defaults to generating when given an ambiguous prompt.

Being aware of this possibility, and reviewing AI generated content with that awareness, is part of responsible usage, particularly for content that will be shared publicly or used to represent an organization.

</details>

<details><summary>Real World Application</summary>

## Responsible Usage in a Team Setting

A development team that adopts AI assisted coding tools typically pairs that adoption with clear expectations: generated code is still reviewed the same way any other code would be, sensitive credentials or proprietary algorithms are not pasted into external tools without approval, and developers remain accountable for the correctness of code they submit, regardless of whether an AI tool helped write it. This framing treats AI tools as a productive addition to an existing, disciplined development process, rather than a replacement for the judgment and review that process already depends on.

</details>

<details><summary>Implementation</summary>

## Sanitizing Input Before Sending a Prompt

```python
import re

def remove_sensitive_data(text):
    # Remove email addresses
    text = re.sub(r"[\w\.-]+@[\w\.-]+\.\w+", "[EMAIL REMOVED]", text)
    # Remove long digit sequences that may be account or card numbers
    text = re.sub(r"\b\d{9,}\b", "[NUMBER REMOVED]", text)
    return text

user_text = "Contact me at person@example.com regarding account 123456789012"
print(remove_sensitive_data(user_text))
```

## A Usage Policy Checklist

```text
Before sending content to an external AI tool:

1. Does this contain customer personal information?
2. Does this contain proprietary code or business logic?
3. Does this contain credentials of any kind?
4. Has this tool been approved for this type of data?
5. Is there a disclosure expectation for the output?

Any yes to items one through three requires either removing
that content or using an approved internal tool.
```

## Reviewing Generated Content Before Use

```python
def pre_publication_review(content):
    review_points = [
        "Have factual claims been verified independently?",
        "Has the content been checked for biased assumptions?",
        "Does the tone match the intended audience?",
        "Is disclosure of AI assistance required here?",
        "Would this pass the same review as human written work?"
    ]
    for point in review_points:
        print(f"[ ] {point}")

pre_publication_review("generated content")
```

## Steps to Follow

1. Check content against the usage policy before sending it.
2. Remove or mask sensitive data from prompts.
3. Review generated output with the same scrutiny as any other draft.
4. Verify factual claims independently before relying on them.
5. Disclose AI assistance where the context expects it.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Responsible AI usage means applying informed judgment about when and how much to rely on these tools.
- Over reliance risks accepting fluent but unverified output without the review it would normally receive.
- Sensitive or confidential information requires care before being included in a prompt sent to an external tool.
- Disclosure expectations around AI assisted work vary by context and should be checked and followed.
- Language models can reflect biases present in their training data, which is worth watching for in generated content.

With responsible use covered at a general level, the next module looks specifically at security best practices when using LLMs in a professional context.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
