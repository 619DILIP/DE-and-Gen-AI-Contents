## Observing Token Based Generation

Text is processed in tokens rather than whole words.

```python
# A rough illustration of how text splits into tokens
text = "unbelievable results today"

# A tokenizer might produce something like:
tokens = ["un", "believ", "able", " results", " today"]
print(len(tokens))
```

Common words often map to a single token, while rarer words split into several.

## Calling a Model and Inspecting the Response

```python
import os
import requests

def generate_text(prompt):
    response = requests.post(
        "https://api.example-llm-service.com/v1/messages",
        headers={
            "Content-Type": "application/json",
            "x-api-key": os.environ.get("LLM_API_KEY")
        },
        json={
            "model": "example-model",
            "max_tokens": 500,
            "messages": [{"role": "user", "content": prompt}]
        }
    )
    return response.json()
```

## Understanding Token Limits

Both the prompt and the response count toward a model's context limit, so long inputs reduce the room available for output.

```python
def estimate_tokens(text):
    # A rough approximation: about four characters per token
    return len(text) // 4

prompt = "Summarize the following report: " + long_document
print(f"Approximate prompt tokens: {estimate_tokens(prompt)}")
```

## Steps to Follow

1. Recognize that prompt and response both consume tokens.
2. Estimate prompt length before sending very large inputs.
3. Set a maximum token limit appropriate to the expected response.
4. Trim unnecessary context rather than sending entire documents.
5. Treat generated output as text produced by pattern prediction, and verify factual claims.
