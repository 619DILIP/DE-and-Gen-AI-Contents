## How an AWS Account Is Normally Set Up

In a workplace, getting access to AWS follows a standard sequence. This is described here so the process is familiar, not as something to carry out now.

1. An account is registered with AWS, which requires billing details.
2. The root account is secured with multi factor authentication immediately, since it has unrestricted access.
3. An administrative IAM user is created for daily work, so the root account is not used routinely.
4. A billing alert is configured so unexpected charges are noticed early.
5. A default region is selected, usually one close to where the data or users are located.

In practice, most people joining a team are handed an IAM user within an account that already exists, rather than creating an account themselves. For this course, no account is needed at all. The Floci module later this week provides a local environment where the commands below run without any AWS account or billing details.

## Installing the AWS CLI

```text
pip install awscli
```

## Configuring Credentials

```text
aws configure
```

This prompts for four values.

```text
AWS Access Key ID:     [access key]
AWS Secret Access Key: [secret key]
Default region name:   us-east-1
Default output format: json
```

Against a local environment such as Floci, the same command is used, but the key values can be any placeholder text, since nothing is authenticating against real AWS.

## Verifying the Setup

```text
aws sts get-caller-identity
```

A successful response confirms the CLI is authenticated and shows which identity is being used.

## Using the SDK from Python

```python
import boto3

# The SDK reads credentials configured by the CLI
s3 = boto3.client("s3")
response = s3.list_buckets()

for bucket in response["Buckets"]:
    print(bucket["Name"])
```