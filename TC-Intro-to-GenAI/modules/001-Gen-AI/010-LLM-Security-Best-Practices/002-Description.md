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
