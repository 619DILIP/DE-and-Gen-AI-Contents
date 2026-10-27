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