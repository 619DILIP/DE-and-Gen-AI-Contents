<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Explain what a local cloud emulator is and why one is used for practice and testing.
- Describe what Floci provides and which AWS services it emulates.
- Install and start Floci on a local machine.
- Configure the AWS CLI and the Python SDK to point at a local Floci endpoint.
- Verify that a local environment is working, and run the same commands covered in the earlier AWS modules against it.
- Recognize where a local emulator differs from real AWS.

</details>

<details><summary>Description</summary>

## Why a Local Environment?

The AWS modules covered so far describe how each service works and what the commands look like. Running those commands against real AWS requires an account with billing details attached, and any resource left running continues to accrue charges until it is shut down.

A local cloud emulator solves this. It runs on a personal machine and responds to the same commands the real service does, so the AWS CLI and the AWS SDK work exactly as they normally would. Nothing is created in the cloud, nothing is billed, and there is no account to secure.

This is not only a training tool. Development teams routinely use local emulators so that automated tests can create and destroy cloud resources on every run, quickly and at no cost, without touching a real environment.

---

## What Is Floci?

Floci is a free, open source local AWS emulator. It runs as a Docker container and exposes AWS compatible services on a single local address. Standard AWS tooling, including the CLI, the Python SDK, and infrastructure as code tools, can be pointed at it and used normally.

The services relevant to this course are all supported:

- **S3** for object storage, including versioning and event notifications
- **Lambda** for serverless functions, run in real Docker containers
- **IAM** for users, roles, policies, and temporary credentials
- **RDS** for relational databases

Because Floci speaks the same protocol as AWS, the commands written in the earlier modules run against it unchanged. A bucket created with `aws s3 mb` behaves the same way, apart from existing only on the local machine.

---

## Prerequisites

Floci runs in Docker, so Docker needs to be installed and running before starting. Verifying this first avoids confusing errors later.

```text
docker --version
```

The AWS CLI is also needed, since it is the primary way of interacting with the services.

```text
aws --version
```

---

## Starting Floci

The simplest approach uses a Docker Compose file. Create a file named `compose.yaml` containing:

```yaml
services:
  floci:
    image: floci/floci:latest
    ports:
      - "4566:4566"
```

Then start it from the same directory:

```text
docker compose up
```

All emulated services become available at `http://localhost:4566`. The first run downloads the image, so it takes longer than subsequent starts.

---

## Configuring the AWS CLI

The CLI needs to know two things: where to send requests, and what credentials to use. Since nothing is authenticating against real AWS, the credential values can be any placeholder text.

```text
export AWS_ENDPOINT_URL=http://localhost:4566
export AWS_DEFAULT_REGION=us-east-1
export AWS_ACCESS_KEY_ID=test
export AWS_SECRET_ACCESS_KEY=test
```

On Windows using PowerShell, the equivalent is:

```text
$env:AWS_ENDPOINT_URL="http://localhost:4566"
$env:AWS_DEFAULT_REGION="us-east-1"
$env:AWS_ACCESS_KEY_ID="test"
$env:AWS_SECRET_ACCESS_KEY="test"
```

These variables apply only to the current terminal session. Opening a new terminal requires setting them again.

---

## Verifying the Setup

A quick check confirms everything is connected before starting any real work.

```text
aws s3 mb s3://test-bucket
aws s3 ls
```

If the bucket is created and then appears in the listing, the environment is working. If the command hangs or reports a connection error, Floci is most likely not running, or the endpoint variable is not set in the current terminal.

---

## Configuring the Python SDK

The Python SDK, `boto3`, needs the same endpoint information. It can be passed directly when creating a client:

```python
import boto3

s3 = boto3.client(
    "s3",
    endpoint_url="http://localhost:4566",
    region_name="us-east-1",
    aws_access_key_id="test",
    aws_secret_access_key="test",
)

s3.create_bucket(Bucket="sales-data")
print([b["Name"] for b in s3.list_buckets()["Buckets"]])
```

Every other `boto3` call covered in the earlier modules works the same way once the client is configured like this. Only the client creation changes.

A practical habit is to read the endpoint from an environment variable, so the same code can run locally or against real AWS without editing:

```python
import os
import boto3

s3 = boto3.client("s3", endpoint_url=os.environ.get("AWS_ENDPOINT_URL"))
```

When `AWS_ENDPOINT_URL` is unset, `boto3` uses real AWS. When it is set to the local address, the same code runs against Floci.

---

## Where a Local Emulator Differs from Real AWS

An emulator reproduces the behavior of a service, not the service itself, so a few differences are worth knowing:

- **Not every feature is supported.** Core operations work, but less common features may be missing or simplified.
- **Performance is not representative.** A local machine is not a distributed system, so timings say nothing about how something would perform at scale.
- **There is no console.** Everything is done through the CLI or the SDK. The AWS Management Console, and the visual walkthrough of creating resources, is covered separately through AWS Cloud Quest.
- **No cost, and therefore no cost feedback.** Because nothing is billed, an inefficient design carries no warning signal. Cost awareness has to be reasoned about rather than observed.

None of these prevent the environment being useful for learning. They are the reason a local emulator complements experience with real AWS rather than fully replacing it.

</details>

<details><summary>Real World Application</summary>

## Emulators in Development and Testing

A team building an application that reads from S3 and writes to a database faces a problem when writing automated tests: creating real cloud resources for every test run is slow, costs money, and risks interfering with a shared environment. Running the same tests against a local emulator lets each run create the buckets and tables it needs, exercise the code fully, and discard everything afterward in seconds.

The same reasoning applies to development. A developer can build and debug against a local environment without needing credentials for a shared account, then deploy to real AWS once the code works. This is why familiarity with local emulation is a practical skill rather than only a training convenience.

</details>

<details><summary>Implementation</summary>

## Full Setup, Step by Step

1. Confirm Docker is installed and running with `docker --version`.
2. Confirm the AWS CLI is installed with `aws --version`.
3. Create a `compose.yaml` file with the Floci service definition.
4. Start the emulator with `docker compose up`.
5. Set the four environment variables in the terminal that will be used for work.
6. Verify with `aws s3 mb s3://test-bucket` followed by `aws s3 ls`.

---

## Working Through the Earlier Modules Locally

The commands from the earlier AWS modules can now be run directly. For example, from the S3 module:

```text
aws s3 mb s3://company-sales-data-example
aws s3 cp orders.csv s3://company-sales-data-example/raw/orders.csv
aws s3 ls s3://company-sales-data-example/raw/
```

From the Cloud Security module:

```text
aws s3api put-bucket-versioning \
    --bucket company-sales-data-example \
    --versioning-configuration Status=Enabled
```

From the IAM module:

```text
aws iam create-role \
    --role-name pipeline-s3-read-role \
    --assume-role-policy-document file://trust-policy.json

aws iam list-roles
```

None of these commands differ from their real AWS equivalents. Only the endpoint they are sent to has changed.

---

## Stopping and Resetting

Stopping the emulator releases the resources it was using.

```text
docker compose down
```

By default, everything created inside Floci is discarded when the container stops. Starting again gives a clean environment. This is useful when an exercise goes wrong, since starting over costs nothing.

---

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| Connection refused | Floci is not running | Check `docker compose up` is active |
| Commands hit real AWS | Endpoint variable not set | Re-export the variables in the current terminal |
| Credential errors | Variables missing | Set placeholder access key and secret |
| Port already in use | Something else is on 4566 | Stop the other process, or map a different port |
| Resources missing after restart | Data is not persisted by default | Expected behavior; recreate them |

---

## A Working Check

Running this short script confirms the whole setup end to end.

```python
import boto3

s3 = boto3.client(
    "s3",
    endpoint_url="http://localhost:4566",
    region_name="us-east-1",
    aws_access_key_id="test",
    aws_secret_access_key="test",
)

s3.create_bucket(Bucket="verify-bucket")
s3.put_object(Bucket="verify-bucket", Key="hello.txt", Body=b"working")

obj = s3.get_object(Bucket="verify-bucket", Key="hello.txt")
print(obj["Body"].read().decode())
```

Output of `working` confirms that creating a bucket, writing an object, and reading it back all function correctly.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- A local cloud emulator responds to standard AWS commands without an account, cloud resources, or cost.
- Floci runs as a Docker container and exposes AWS compatible services at `http://localhost:4566`.
- The AWS CLI is pointed at it by setting an endpoint variable and placeholder credentials.
- The Python SDK is pointed at it by passing `endpoint_url` when creating a client.
- Commands from the earlier AWS modules run against it unchanged.
- An emulator differs from real AWS in feature coverage, performance, and the absence of a console, which is why it complements rather than replaces cloud experience.

With a working local environment, the practical exercises for this section can be completed safely, at no cost and without an AWS account.

This closes out the cloud and AWS content. The next section shifts into an entirely new area, an introduction to artificial intelligence and generative AI.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
