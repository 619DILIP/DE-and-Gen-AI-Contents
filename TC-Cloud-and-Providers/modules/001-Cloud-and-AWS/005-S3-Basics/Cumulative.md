<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Define Amazon S3 and explain what type of storage it provides.
- Explain the concepts of buckets and objects.
- Identify common use cases for S3 within a data pipeline.
- Describe how access to an S3 bucket is controlled.
- Recognize why S3 is a common choice for data lake style storage.

> **Before you start**
>
> This module walks through the process so you understand how the service works and what the steps involve. **You do not need to do any of this hands on right now, and you should not create a personal AWS account to follow along.**
>
> Hands on practice comes later this week, once the Floci module introduces a local environment where you can run all of these commands safely, at no cost, without an AWS account. Read through the steps here, then apply them there.

</details>

<details><summary>Description</summary>

## What Is S3?

Amazon Simple Storage Service, known as S3, is AWS's object storage service. Unlike RDS, which stores structured data in database tables, S3 stores files, called objects, in a flat storage structure without requiring any predefined schema. This makes it well suited to storing data in any format, structured, semi structured, or unstructured, which connects directly to the data lake concept covered earlier.

---

## Buckets and Objects

S3 storage is organized around two core concepts:

- **Buckets**: Top level containers that hold objects. A bucket name must be globally unique across all of AWS, since bucket names form part of the resulting storage address.
- **Objects**: The individual files stored within a bucket, along with metadata describing them. An object can be nearly any file type: a CSV file, a JSON file, an image, a video, or a compressed archive.

```text
Bucket: company-sales-data
    ├── raw/2024-01-15/orders.csv
    ├── raw/2024-01-16/orders.csv
    └── processed/summary.json
```

Although S3 does not have real folders in the traditional sense, object names commonly include forward slashes, which most tools and the AWS console display as a folder like structure for organizational convenience.

---

## Common Use Cases

S3 is widely used for:

- **Raw data storage**: Holding unprocessed data as it arrives from various sources, before it is cleaned and loaded into a warehouse.
- **Data lake storage**: Serving as the underlying storage layer for a data lake, given its low cost and support for any file format.
- **Backups and archives**: Storing backup copies of data or systems for long term retention.
- **Static file hosting**: Serving files directly, such as website assets or downloadable reports.

Within a data pipeline, S3 is commonly the landing zone where raw extracted data is written first, before a transformation process reads it, cleans it, and loads it into a database such as RDS or a dedicated data warehouse platform.

---

## Access Control

Access to S3 buckets and objects is controlled through a combination of bucket policies and IAM permissions, the latter covered in more detail in the next module. By default, a newly created S3 bucket is private, accessible only to the AWS account that created it. Public access must be explicitly granted, and AWS provides safeguards specifically designed to prevent buckets from being made public accidentally, since misconfigured public buckets have historically been a common source of data exposure.

---

## Cost Characteristics

S3 is priced based on the amount of data stored, the number of requests made against it, and the amount of data transferred out of it. Because storage cost per unit is relatively low compared to a structured database, S3 is a natural fit for storing large volumes of raw or infrequently accessed data.

</details>

<details><summary>Real World Application</summary>

## S3 as a Data Lake Landing Zone

A data engineering team building a nightly pipeline commonly configures the extraction step to write raw data directly into an S3 bucket first, organized by date, before any transformation happens. This gives the team a permanent, low cost copy of the exact raw data that was received on any given day. If a bug is later discovered in the transformation logic, the team can reprocess the original raw files sitting in S3 without needing to re extract that data from the original source systems, which may not always have historical data readily available.

</details>

<details><summary>Implementation</summary>

## Creating a Bucket

```text
aws s3 mb s3://company-sales-data-example
```

Bucket names must be globally unique across all AWS accounts.

## Uploading and Downloading Files

```text
# Upload a single file
aws s3 cp orders.csv s3://company-sales-data-example/raw/orders.csv

# Download a file
aws s3 cp s3://company-sales-data-example/raw/orders.csv ./orders.csv

# List bucket contents
aws s3 ls s3://company-sales-data-example/raw/
```

## Working with S3 from Python

```python
import boto3

s3 = boto3.client("s3")
BUCKET = "company-sales-data-example"

# Upload
s3.upload_file("orders.csv", BUCKET, "raw/2024/01/orders.csv")

# Download
s3.download_file(BUCKET, "raw/2024/01/orders.csv", "local_orders.csv")

# List objects under a prefix
response = s3.list_objects_v2(Bucket=BUCKET, Prefix="raw/2024/")
for obj in response.get("Contents", []):
    print(obj["Key"], obj["Size"])
```

## Reading a File Without Downloading It

```python
response = s3.get_object(Bucket=BUCKET, Key="raw/2024/01/orders.csv")
content = response["Body"].read().decode("utf-8")

for line in content.splitlines()[:5]:
    print(line)
```

## Organizing by Date

```python
from datetime import datetime

def build_key(prefix, filename):
    now = datetime.now()
    return f"{prefix}/year={now.year}/month={now.month:02d}/{filename}"

key = build_key("raw/orders", "orders.csv")
s3.upload_file("orders.csv", BUCKET, key)
```

## Steps to Follow

1. Create a bucket with a clear, unique name.
2. Confirm the bucket is private, which is the default.
3. Define a consistent key naming convention before uploading data.
4. Upload files using the CLI or the SDK.
5. Enable encryption and versioning on buckets holding important data.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- S3 is AWS's object storage service, storing files without requiring a predefined schema.
- Storage in S3 is organized into buckets, which contain individual objects.
- S3 is commonly used for raw data storage, data lakes, backups, and static file hosting.
- Access to S3 is private by default and controlled through bucket policies and IAM permissions.
- S3's low storage cost makes it a natural landing zone for raw pipeline data.

With compute, database, and storage covered, the next module looks at how access to all of these services is controlled through AWS IAM.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
