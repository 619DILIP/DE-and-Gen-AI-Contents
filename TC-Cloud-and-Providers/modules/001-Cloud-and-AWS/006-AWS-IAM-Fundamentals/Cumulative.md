<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Define AWS IAM and explain the problem it solves.
- Distinguish between IAM users, groups, and roles.
- Explain what an IAM policy is and how permissions are granted.
- Describe the principle of least privilege and why it matters.
- Recognize common IAM misconfigurations to avoid.

> **Before you start**
>
> This module walks through the process so you understand how the service works and what the steps involve. **You do not need to do any of this hands on right now, and you should not create a personal AWS account to follow along.**
>
> Hands on practice comes later this week, once the Floci module introduces a local environment where you can run all of these commands safely, at no cost, without an AWS account. Read through the steps here, then apply them there.

</details>

<details><summary>Description</summary>

## What Is IAM?

AWS Identity and Access Management, known as IAM, is the service that controls who can access AWS resources and what they are allowed to do with them. Every action taken within an AWS account, launching an EC2 instance, reading an S3 object, connecting to an RDS database, is checked against IAM permissions before it is allowed to happen.

---

## Users, Groups, and Roles

IAM organizes identities and permissions using a few core concepts:

- **Users**: Represent an individual person or application that needs to interact with AWS directly, each with their own credentials.
- **Groups**: Collections of users that share the same set of permissions, making it easier to manage permissions for many users at once rather than individually.
- **Roles**: A set of permissions that can be temporarily assumed, commonly used to grant an AWS service, such as an EC2 instance, permission to access other services, such as S3, without needing to store permanent credentials directly on that instance.

Roles are especially important in a data engineering context. An EC2 instance or a Lambda function running a pipeline is typically assigned a role that grants it exactly the permissions it needs, for example the ability to read from a specific S3 bucket and write to a specific RDS database, without embedding any long lived credentials in the pipeline code itself. In the case of Lambda this is called the execution role, covered later in this section.

---

## Policies

Permissions in IAM are defined using policies, which are documents that specify what actions are allowed or denied on which resources. A simple policy might grant permission to read objects from a specific S3 bucket, but deny permission to delete anything from it.

```text
Effect: Allow
Action: s3:GetObject
Resource: arn:aws:s3:::company-sales-data/*
```

This example policy allows reading objects from the `company-sales-data` bucket, but does not grant any other permissions, such as the ability to delete objects or access a different bucket.

---

## The Principle of Least Privilege

A foundational security concept in IAM, and in cloud security generally, is the principle of least privilege: every user, application, or role should be granted only the specific permissions it needs to do its job, and nothing more.

Following this principle limits the potential damage if credentials are ever compromised or if a mistake is made in code. A pipeline that only has permission to read from one specific S3 bucket cannot accidentally, or maliciously, delete data from an unrelated bucket, simply because it was never granted that permission in the first place.

---

## Common Misconfigurations

Some of the most common and consequential security issues in cloud environments come from IAM misconfigurations, including:

- Granting overly broad permissions, such as full administrative access, when a much narrower set of permissions would suffice.
- Embedding long lived credentials directly in application code instead of using roles.
- Failing to remove permissions from users or roles that no longer need them.

These are not obscure edge cases. They are consistently among the leading causes of real world cloud security incidents, which is why IAM is treated as a foundational, not optional, part of working with AWS.

</details>

<details><summary>Real World Application</summary>

## Assigning a Role to a Pipeline

Rather than hardcoding an AWS access key and secret directly into a data pipeline's code, a data engineering team assigns an IAM role to the EC2 instance running the pipeline. That role is configured with a narrowly scoped policy, granting only the specific S3 and RDS permissions the pipeline actually needs. If the pipeline code is ever accidentally exposed, for example checked into a shared code repository by mistake, there are no embedded credentials to be misused, since the permissions are tied to the role assigned to the instance rather than to a secret stored in the code.

</details>

<details><summary>Implementation</summary>

## Writing a Narrow Policy

A policy granting read only access to one specific bucket.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::company-sales-data-example",
                "arn:aws:s3:::company-sales-data-example/*"
            ]
        }
    ]
}
```

Both the bucket itself and the objects within it are listed, since listing a bucket and reading its objects are separate permissions.

## Creating a Role for an EC2 Instance

1. Open the IAM service in the AWS Management Console.
2. Create a new role and select EC2 as the trusted service.
3. Attach the narrow policy defined above.
4. Give the role a descriptive name, such as `pipeline-s3-read-role`.
5. Attach the role to the EC2 instance running the pipeline.

## Using the Role from Code

No credentials appear in the code. The SDK retrieves temporary credentials from the attached role automatically.

```python
import boto3

# No keys passed in, credentials come from the instance role
s3 = boto3.client("s3")
response = s3.get_object(
    Bucket="company-sales-data-example",
    Key="raw/orders.csv"
)
```

## Verifying Permissions

```text
aws sts get-caller-identity
aws s3 ls s3://company-sales-data-example/
```

Attempting an action outside the policy should fail, which confirms the permissions are correctly scoped.

## Steps to Follow

1. List exactly which actions the application needs to perform.
2. Write a policy granting only those actions on only those resources.
3. Create a role and attach that policy.
4. Assign the role to the service that needs it.
5. Test that permitted actions succeed and non permitted actions fail.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- IAM controls who can access AWS resources and what actions they are allowed to perform.
- Users, groups, and roles represent different ways of organizing identities and permissions.
- Policies define specific allowed or denied actions on specific resources.
- The principle of least privilege limits permissions to exactly what is needed, reducing potential damage from mistakes or compromised credentials.
- Overly broad permissions and hardcoded credentials are common, high impact security misconfigurations.

With core services and access control covered, the next module looks at broader cloud security practices that build on these IAM concepts.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
