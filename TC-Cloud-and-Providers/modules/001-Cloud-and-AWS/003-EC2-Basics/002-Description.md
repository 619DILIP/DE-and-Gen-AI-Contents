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