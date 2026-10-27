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