<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Define an AWS region and explain why resources belong to one.
- Define an availability zone and explain the purpose of physical separation.
- Describe the relationship between regions, availability zones, and edge locations.
- Identify the factors that drive a region choice.
- Explain how spreading resources across availability zones provides fault tolerance.
- Recognize why a resource can appear to be missing when the region is wrong.

> **Before you start**
>
> This module walks through the process so you understand how the service works and what the steps involve. **You do not need to do any of this hands on right now, and you should not create a personal AWS account to follow along.**
>
> Hands on practice comes later this week, once the Floci module introduces a local environment where you can run all of these commands safely, at no cost, without an AWS account. Read through the steps here, then apply them there.

</details>

<details><summary>Description</summary>

## AWS Is Not One Place

It is easy to think of the cloud as a single system somewhere. In practice, AWS runs physical data centers in locations around the world, and that geography is exposed directly to anyone using it. Almost every decision made when creating a resource involves choosing where it lives.

Understanding this structure early explains a set of behaviors that otherwise seem arbitrary, and it prevents a category of mistakes that are awkward to undo.

---

## Regions

A region is a separate geographic area containing its own AWS infrastructure. Examples include one in Northern Virginia, one in Ireland, one in Mumbai, and one in Sydney. Each region has a code used in commands and configuration, such as `us-east-1`, `eu-west-1`, or `ap-south-1`.

The important property is that regions are independent of one another. Three consequences follow directly:

- **Resources belong to a region.** A storage bucket created in Ireland does not appear when looking at the Mumbai region. This is why almost every command and console screen involves a region, and why a resource can seem to have disappeared when the region has been switched by accident.
- **Pricing varies by region.** The same service can cost different amounts depending on where it runs, sometimes noticeably.
- **Service availability varies.** Newer services often launch in a small number of regions and expand later, so a service available in one region may not yet exist in another.

---

## Choosing a Region

Three considerations usually drive the decision.

**Latency.** Data travels at a finite speed, so physical distance matters. An application serving users in Europe will respond faster from a European region than from one in North America. The usual guidance is to run close to whoever or whatever is using the service.

**Compliance and data residency.** Some data is legally required to remain within a particular country or jurisdiction. Where regulations require personal data to stay within a specific area, the region choice is not a preference but a requirement, and it is often the deciding factor regardless of cost or latency.

**Cost.** Regions are priced differently. A more distant region may be cheaper, which can be worth it for workloads where nobody is waiting on a response, such as overnight batch processing or long term archival.

These can conflict. A cheaper region may be the wrong one for compliance, or the compliant region may not be the closest. Naming which of the three is the constraint usually settles the decision quickly.

---

## Availability Zones

Within a region, infrastructure is divided further into availability zones. An availability zone is one or more physically separate data centers with independent power, cooling, and networking.

```text
Region: us-east-1
    |
    +-- Availability Zone us-east-1a     independent power and networking
    +-- Availability Zone us-east-1b     independent power and networking
    +-- Availability Zone us-east-1c     independent power and networking
```

The separation is deliberate and carefully balanced. Zones are far enough apart that a localized problem, such as a power failure, a fire, or a flood, is unlikely to affect more than one at a time. They are close enough together that the network links between them are fast, so an application spread across zones does not pay a meaningful latency penalty for the arrangement.

Most regions contain at least three availability zones.

---

## Why Availability Zones Exist

Hardware fails. Data centers occasionally lose power. Availability zones exist so that those events do not have to take an application down with them.

An application running in a single zone has a single point of failure. The same application running across two or more zones can keep serving from the remaining zones when one becomes unreachable.

This is the reasoning behind patterns that appear repeatedly across AWS services:

- A database configured for high availability maintains a standby copy in a second availability zone and switches to it automatically if the primary becomes unreachable.
- A group of servers behind a load balancer is normally distributed across zones, so the load balancer can route around a zone that stops responding.
- Storage services replicate data across multiple zones by default, which is why an object put into storage survives the loss of a data center without anything being configured.

The cost of designing this way at the outset is usually small. The cost of retrofitting it after an outage is considerably higher.

---

## Edge Locations

A third type of location is worth knowing about, though it is used differently. Edge locations are a much larger number of smaller sites, placed close to end users, that cache content rather than run applications. Their purpose is to serve frequently requested content from somewhere physically near the person requesting it, rather than fetching it from the region each time.

Regions and availability zones are where infrastructure runs. Edge locations are where content is cached for speed.

---

## Why the Choice Matters Early

Region and availability zone decisions are made at the moment a resource is created, and some are difficult to reverse. Moving a database to a different region is a migration involving planning and downtime, not a setting to be changed. Choosing deliberately at the start avoids that work later.

</details>

<details><summary>Real World Application</summary>

## Designing for Geography and Failure

A company serving customers primarily in Europe would normally run its workloads in a European region. The latency is lower for those users, and data protection rules may require personal data to remain within the region regardless of any other consideration.

Within that region, anything that needs to stay available is distributed across availability zones. The application servers are spread across at least two, and the database runs with a standby in a second zone. A single zone becoming unavailable degrades capacity rather than stopping the service.

Separately, backups are often replicated to a second region. Availability zones protect against the loss of a data center; a second region protects against a problem affecting an entire geographic area. The two serve different purposes, and a design concerned with continuity usually accounts for both.

</details>

<details><summary>Implementation</summary>

## Checking the Configured Region

The region set during configuration applies to every command unless it is overridden.

```text
aws configure get region
```

```text
us-east-1
```

---

## Listing Regions and Zones

Which regions are available to an account:

```text
aws ec2 describe-regions --output table
```

Which availability zones exist within a given region:

```text
aws ec2 describe-availability-zones --region us-east-1 --output table
```

The zone names returned follow the region code with a letter appended, such as `us-east-1a` and `us-east-1b`.

---

## Overriding the Region for a Single Command

A command can target a different region without changing the default.

```text
aws s3 ls --region eu-west-1
```

This is useful when working across regions, and it is also the quickest way to check whether a resource that appears to be missing is simply somewhere else.

---

## Setting the Region in Code

The Python SDK takes the region when a client is created.

```python
import boto3

s3_virginia = boto3.client("s3", region_name="us-east-1")
s3_ireland  = boto3.client("s3", region_name="eu-west-1")

# These list different sets of resources
print(s3_virginia.list_buckets())
```

Reading it from configuration rather than hardcoding keeps the same code usable across environments:

```python
import os
import boto3

client = boto3.client("s3", region_name=os.environ.get("AWS_DEFAULT_REGION", "us-east-1"))
```

---

## Creating a Resource in a Specific Region

```text
aws s3 mb s3://company-sales-data-example --region eu-west-1
```

Listing buckets from a different region will not show it, which is expected behavior rather than an error.

---

## Diagnosing a Missing Resource

When a resource that was definitely created cannot be found, work through this in order:

1. Check the configured region with `aws configure get region`.
2. Check which region the resource was created in.
3. Re-run the command with `--region` set to that region.
4. If it appears, the resource was never missing; the region was wrong.

This is one of the most common sources of confusion when starting with AWS, and it is worth checking before assuming anything more complicated has gone wrong.

---

## Steps to Follow

1. Decide which of latency, compliance, or cost is the binding constraint for the workload.
2. Choose a region on that basis, and confirm the services needed are available there.
3. Set that region as the configured default so commands do not need it repeated.
4. For anything that must stay available, distribute resources across at least two availability zones.
5. Consider replicating backups to a second region for protection against a region wide problem.
6. When a resource appears to be missing, check the region before anything else.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- A region is an independent geographic area with its own AWS infrastructure, identified by a code such as `us-east-1`.
- Resources belong to a region, so the selected region determines what is visible, what it costs, and which services are available.
- Region choice is driven by latency, compliance and data residency requirements, and cost.
- An availability zone is one or more physically separate data centers within a region, with independent power and networking.
- Distributing resources across availability zones is how AWS workloads tolerate the failure of a single data center.
- Edge locations cache content close to users and are distinct from regions and availability zones, which run infrastructure.
- Region and zone choices are made at creation time and some are difficult to reverse, so they are worth deciding deliberately.

With the geographic structure understood, the next module looks at Amazon EC2, the virtual server service that most long running workloads use.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>