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