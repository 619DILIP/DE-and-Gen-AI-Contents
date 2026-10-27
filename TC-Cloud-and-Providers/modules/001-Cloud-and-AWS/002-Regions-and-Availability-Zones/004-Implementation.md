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