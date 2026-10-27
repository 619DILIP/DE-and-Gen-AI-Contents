In this module, we learned:

- A local cloud emulator responds to standard AWS commands without an account, cloud resources, or cost.
- Floci runs as a Docker container and exposes AWS compatible services at `http://localhost:4566`.
- The AWS CLI is pointed at it by setting an endpoint variable and placeholder credentials.
- The Python SDK is pointed at it by passing `endpoint_url` when creating a client.
- Commands from the earlier AWS modules run against it unchanged.
- An emulator differs from real AWS in feature coverage, performance, and the absence of a console, which is why it complements rather than replaces cloud experience.

With a working local environment, the practical exercises for this section can be completed safely, at no cost and without an AWS account.

This closes out the cloud and AWS content. The next section shifts into an entirely new area, an introduction to artificial intelligence and generative AI.