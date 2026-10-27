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