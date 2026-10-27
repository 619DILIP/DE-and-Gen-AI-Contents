<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Explain what Amazon Web Services is and its position in the cloud computing market.
- Identify the major categories of AWS services.
- Describe the AWS shared responsibility model.
- Recognize how AWS services are typically accessed.
- Explain how AWS pricing generally works.

> **Before you start**
>
> This module walks through the process so you understand how the service works and what the steps involve. **You do not need to do any of this hands on right now, and you should not create a personal AWS account to follow along.**
>
> Hands on practice comes later this week, once the Floci module introduces a local environment where you can run all of these commands safely, at no cost, without an AWS account. Read through the steps here, then apply them there.

</details>

<details><summary>Description</summary>

## What Is AWS?

Amazon Web Services, commonly known as AWS, is a cloud computing platform that provides on demand access to computing power, storage, databases, and hundreds of other services, all delivered over the internet and billed based on usage. Rather than an organization purchasing and maintaining its own physical servers, AWS allows that same computing capability to be rented as needed.

AWS is one of the largest cloud providers in the world, alongside Microsoft Azure and Google Cloud. The concepts and services introduced in this section, while specific to AWS, mirror equivalent offerings across other major cloud providers.

---

## Categories of AWS Services

AWS offers an extensive catalog of services, but most fall into a small number of broad categories relevant to this section:

- **Compute**: Services that run application code and processes, most notably Amazon EC2 for virtual servers and AWS Lambda for event driven functions, both covered in this section.
- **Storage**: Services that store files and data, most notably Amazon S3.
- **Database**: Managed database services, most notably Amazon RDS.
- **Security and Access Management**: Services that control who can do what within an AWS account, most notably AWS IAM.

Understanding these four categories provides enough of a foundation to reason about how most cloud based systems are built, even without knowing the full breadth of AWS's service catalog.

---

## The Shared Responsibility Model

A key concept for understanding cloud security is the shared responsibility model. AWS is responsible for the security of the underlying cloud infrastructure itself, physical data centers, networking hardware, and the virtualization layer. The customer using AWS is responsible for security within that infrastructure, including how they configure their services, who has access, and how their own application data is protected.

In simple terms, AWS secures the cloud itself, while the customer is responsible for what they build and configure inside it. This distinction matters throughout this section, particularly when covering IAM and security best practices.

---

## Accessing AWS Services

AWS services can be accessed in a few common ways:

- **AWS Management Console**: A web based graphical interface for manually creating and managing resources.
- **AWS Command Line Interface (CLI)**: A tool for managing AWS resources through terminal commands, useful for automation and repeatable setups.
- **Software Development Kits (SDKs)**: Libraries that allow application code, including Python code, to interact directly with AWS services programmatically.

Most learners are introduced to AWS through the Management Console first, since it provides a visual way to understand what a service does before working with it through code or automation.

---

## How AWS Pricing Works

AWS generally follows a pay as you go pricing model. Rather than a fixed monthly fee regardless of usage, costs are typically based on factors such as how much compute time was used, how much data was stored, and how much data was transferred. This is one of the main appeals of cloud computing: an organization pays only for what it actually uses, and can scale usage up or down as needs change, without the fixed cost of maintaining owned hardware.

</details>

<details><summary>Real World Application</summary>

## Why Companies Choose AWS

A startup building a new application does not need to purchase, configure, and maintain physical servers before writing a single line of code. Instead, it can provision the compute and storage it needs on AWS within minutes, pay only for what it uses, and scale that infrastructure up automatically if the application grows in popularity. This ability to start small and scale on demand, without large upfront infrastructure investment, is one of the primary reasons cloud platforms like AWS have become the default choice for most new software projects.

</details>

<details><summary>Implementation</summary>

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

</details>

<details><summary>Summary</summary>

In this module, we learned:

- AWS is a cloud computing platform providing on demand compute, storage, and other services over the internet.
- AWS services broadly fall into categories including compute, storage, database, and security.
- The shared responsibility model divides security duties between AWS and the customer.
- AWS can be accessed through the Management Console, the CLI, or SDKs.
- AWS pricing is generally usage based rather than a fixed cost.

With this foundation, the next module looks at how AWS organizes its infrastructure geographically, into regions and availability zones.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>