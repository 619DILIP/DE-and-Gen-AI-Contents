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
