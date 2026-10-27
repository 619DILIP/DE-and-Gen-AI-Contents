<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Explain how to securely manage API keys when integrating with an LLM service.
- Describe the importance of validating and reviewing LLM generated output before acting on it.
- Identify why AI generated code or commands should never be executed automatically without review.
- Explain the role of rate limiting and usage monitoring when using LLM APIs.
- Apply access control principles to systems that integrate LLM functionality.

</details>

<details><summary>Description</summary>

## Securing API Keys

Most LLM services are accessed programmatically through an API, authenticated using an API key. This key should be handled with the same care as any other sensitive credential:

- Never hardcode an API key directly in application code, particularly code that might be committed to a shared repository.
- Store keys using environment variables or a dedicated secrets management service, consistent with the credential handling practices covered in the AWS IAM module.
- Restrict which parts of a system have access to a given key, following the principle of least privilege.

```python
import os

api_key = os.environ.get("LLM_API_KEY")
```

Loading a key from an environment variable, rather than writing it directly into the source code, is a simple but effective habit that prevents credentials from ending up somewhere they should not be, such as a public code repository.

---

## Validating Output Before Acting On It

Building directly on the earlier modules covering hallucinations and code generation risks, a critical security practice is never automatically executing or acting on LLM generated output without review, particularly output that takes the form of code, commands, or instructions to another system.

This matters specifically because a model can generate output that looks correct and reasonable while actually being incorrect, harmful, or unsafe, without any indication that anything is wrong. A system designed to take an LLM's output and automatically execute it, for example running a generated database query or a generated shell command without any human or automated safety check in between, introduces significant risk that would not exist if that output were reviewed first.

```text
Risky pattern:
LLM generates a SQL query  →  Query is executed directly against
a production database with no review or validation

Safer pattern:
LLM generates a SQL query  →  Query is reviewed, validated against
expected structure, and run against a test environment first
```

---

## Rate Limiting and Usage Monitoring

LLM APIs are typically billed based on usage, and they can also be a target for abuse if not properly controlled, for example if a public facing feature that calls an LLM API is exploited to generate excessive, costly requests. Practical safeguards include:

- Setting rate limits on how frequently a given user or system can make requests.
- Monitoring usage patterns to detect unusual spikes that might indicate misuse.
- Setting billing alerts or hard usage caps to prevent unexpectedly large costs from an unforeseen usage pattern.

---

## Access Control for LLM Integrated Systems

When an LLM is integrated into a larger system, for example a support tool that can query internal data to help answer customer questions, the same access control principles covered in the IAM module apply directly. The LLM component of that system should only have access to the specific data it needs to perform its function, and any action it can trigger, such as looking up an order or updating a record, should be scoped as narrowly as possible, consistent with the principle of least privilege.

---

## Bringing It Together

These practices are not unique or unusual security concepts invented specifically for AI. They are the same fundamental security principles covered earlier in this section, credential management, least privilege access, and careful validation before acting on untrusted input, applied specifically to the context of LLM integration. Treating LLM security as an extension of standard security practice, rather than an entirely separate discipline, is the most reliable way to apply these principles consistently.

</details>

<details><summary>Real World Application</summary>

## Building an LLM Powered Feature Safely

A team building a feature that uses an LLM to help generate database queries from natural language questions applies these practices together: the API key used to call the LLM service is stored securely and never exposed in client side code, generated queries are validated against an allow list of permitted operations before execution, rather than run directly, and usage is monitored to catch any unexpected spikes in request volume. None of these steps eliminate the underlying uncertainty in what the model generates, but together they ensure that uncertainty cannot translate directly into an unreviewed action against a production system.

</details>

<details><summary>Implementation</summary>

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

</details>

<details><summary>Summary</summary>

In this module, we learned:

- API keys for LLM services should be stored securely, never hardcoded directly into application code.
- LLM generated output, particularly code or commands, should be validated and reviewed before being executed automatically.
- Rate limiting and usage monitoring help control cost and detect potential misuse of LLM API access.
- Access control principles, such as least privilege, apply directly to systems that integrate LLM functionality.
- LLM security largely applies established security principles to a new context, rather than requiring an entirely separate approach.

With LLM specific security practices covered, the next module looks more broadly at security considerations across AI tooling.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
