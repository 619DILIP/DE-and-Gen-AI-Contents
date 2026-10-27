## Loading an API Key Securely

```python
import os

def get_api_key():
    key = os.environ.get("LLM_API_KEY")
    if not key:
        raise RuntimeError(
            "LLM_API_KEY is not set. Configure it as an "
            "environment variable before running."
        )
    return key
```

Setting the variable outside the code.

```text
export LLM_API_KEY="your-key-here"
```

## Excluding Secrets from Version Control

```text
# .gitignore
.env
*.pem
credentials.json
```

## Adding Rate Limiting

```python
import time

class RateLimiter:
    def __init__(self, max_calls, period_seconds):
        self.max_calls = max_calls
        self.period = period_seconds
        self.calls = []

    def allow(self):
        now = time.time()
        self.calls = [t for t in self.calls if now - t < self.period]
        if len(self.calls) >= self.max_calls:
            return False
        self.calls.append(now)
        return True

limiter = RateLimiter(max_calls=10, period_seconds=60)

if limiter.allow():
    print("Request permitted")
else:
    print("Rate limit exceeded")
```

## Validating Generated Queries

```python
def validate_before_execution(generated_sql, allowed_tables):
    normalized = generated_sql.upper()
    if not normalized.strip().startswith("SELECT"):
        raise ValueError("Only SELECT statements are permitted")
    if not any(table.upper() in normalized for table in allowed_tables):
        raise ValueError("Query references an unapproved table")
    return generated_sql
```

## Steps to Follow

1. Store API keys in environment variables or a secrets manager.
2. Add credential files to version control exclusions.
3. Apply rate limits to any user facing feature calling an LLM API.
4. Validate generated code or queries before executing them.
5. Set billing alerts to catch unexpected usage spikes.
