<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Define Amazon EC2 and explain what problem it solves.
- Identify the key configuration choices made when launching an EC2 instance.
- Explain the concept of an instance type and how it affects cost and performance.
- Describe how instances are accessed once running.
- Recognize common use cases for EC2 in a data engineering context.

> **Before you start**
>
> This module walks through the process so you understand how the service works and what the steps involve. **You do not need to do any of this hands on right now, and you should not create a personal AWS account to follow along.**
>
> Hands on practice comes later this week, once the Floci module introduces a local environment where you can run all of these commands safely, at no cost, without an AWS account. Read through the steps here, then apply them there.

</details>

<details><summary>Description</summary>

## What Is EC2?

Amazon Elastic Compute Cloud, known as EC2, is AWS's core compute service. It provides virtual servers, called instances, that can be launched on demand and used to run almost any kind of application or process, from a simple script to a full web application.

Before services like EC2 existed, running an application meant purchasing and physically maintaining a server. EC2 removes that requirement entirely: an instance can be launched in minutes, used for as long as needed, and shut down when it is no longer required, with billing based on the time it was actually running.

---

## Key Configuration Choices

Launching an EC2 instance involves a handful of important decisions:

- **Amazon Machine Image (AMI)**: A template that defines the operating system and any pre installed software the instance starts with, such as a specific Linux distribution.
- **Instance Type**: Determines the amount of CPU, memory, and network performance available. Instance types are named using a combination of a family and size, for example `t3.micro` or `m5.large`, where the family indicates the general balance of resources and the size indicates how much of each.
- **Storage**: Attached storage volumes, which persist data even when the instance itself is stopped.
- **Security Group**: A set of firewall rules controlling what network traffic is allowed to reach the instance.
- **Key Pair**: A cryptographic key used to securely connect to the instance after it launches, instead of a traditional username and password.

---

## Instance Types and Cost

Instance types are grouped into families optimized for different workloads:

- **General purpose** instances balance compute, memory, and networking, suitable for a wide range of applications.
- **Compute optimized** instances provide more CPU power relative to memory, suited for processing intensive workloads.
- **Memory optimized** instances provide more memory relative to CPU, suited for workloads such as large in memory databases.

Cost scales directly with the resources an instance type provides. A small `t3.micro` instance costs a small fraction of what a larger instance with significantly more CPU and memory would cost per hour. Choosing an instance type that matches the actual workload, rather than defaulting to the largest available option, is a standard cost management practice.

---

## Connecting to an Instance

Once an instance is running, it is typically accessed using SSH, a secure remote connection protocol, authenticated using the key pair selected when the instance was launched. From that point, the instance behaves like any other Linux or Windows machine, accessible remotely, where software can be installed and commands can be run directly.

```text
Local Machine  →  SSH connection (using key pair)  →  Running EC2 Instance
```

---

## EC2 in a Data Engineering Context

Within a data pipeline, an EC2 instance is commonly used to run extraction and transformation code on a schedule. Rather than running that code on a personal laptop, which would need to be left running and connected to the internet continuously, the code runs on an EC2 instance that can be scheduled to start, run the pipeline, and stop automatically.

This is the scheduled, batch style of pipeline. Work that instead needs to run the moment data arrives is usually better suited to AWS Lambda, covered later in this section, which runs only in response to an event rather than on a fixed timetable.

</details>

<details><summary>Real World Application</summary>

## Right Sizing a Workload

A data engineering team running a nightly pipeline that processes a moderate volume of data does not need the largest, most expensive instance type available. Instead, the team typically tests the pipeline against a few instance types, measures how long each takes to complete the job, and selects the smallest instance type that finishes the work within an acceptable time window. This practice, often called right sizing, is a common and effective way to control cloud costs without sacrificing the reliability of scheduled jobs.

</details>

<details><summary>Implementation</summary>

## Launching an Instance from the Console

1. Open the EC2 service in the AWS Management Console.
2. Select an Amazon Machine Image, such as an Amazon Linux distribution.
3. Choose an instance type, starting with a small type for testing.
4. Create or select a key pair, and download the private key file.
5. Configure a security group allowing SSH access from a known IP address.
6. Launch the instance and wait for its status to become running.

## Connecting to the Instance

```text
chmod 400 my-key.pem
ssh -i my-key.pem ec2-user@<public-ip-address>
```

The `chmod` step restricts the key file permissions, which SSH requires before it will use the key.

## Setting Up a Python Environment

```text
sudo yum update -y
sudo yum install python3 -y
python3 --version
```

## Running a Pipeline Script

```text
# Copy the script to the instance
scp -i my-key.pem pipeline.py ec2-user@<public-ip-address>:~/

# Run it on the instance
ssh -i my-key.pem ec2-user@<public-ip-address>
python3 pipeline.py
```

## Launching an Instance with the CLI

```text
aws ec2 run-instances \
    --image-id ami-xxxxxxxxxxxx \
    --instance-type t3.micro \
    --key-name my-key \
    --security-group-ids sg-xxxxxxxxxxxx
```

## Stopping an Instance

Billing continues while an instance runs, so stopping it when not in use controls cost.

```text
aws ec2 stop-instances --instance-ids i-xxxxxxxxxxxx
```

</details>

<details><summary>Summary</summary>

In this module, we learned:

- EC2 provides on demand virtual servers, called instances, billed based on usage.
- Launching an instance requires choosing an AMI, an instance type, storage, a security group, and a key pair.
- Instance types are grouped into families optimized for general purpose, compute intensive, or memory intensive workloads.
- Instances are typically accessed remotely using SSH and a key pair.
- EC2 instances are commonly used to run the extraction and transformation code within a data pipeline.

With compute covered, the next module looks at Amazon RDS, the managed database service commonly paired with EC2 in data driven applications.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
