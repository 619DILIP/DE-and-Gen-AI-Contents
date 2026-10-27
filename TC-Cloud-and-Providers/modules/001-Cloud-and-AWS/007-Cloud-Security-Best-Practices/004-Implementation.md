## Restricting a Security Group

```text
# Allow SSH from one specific address only
aws ec2 authorize-security-group-ingress \
    --group-id sg-xxxxxxxxxxxx \
    --protocol tcp \
    --port 22 \
    --cidr 203.0.113.25/32
```

Using a single address rather than an open range limits who can reach the instance.

## Enabling S3 Encryption

```text
aws s3api put-bucket-encryption \
    --bucket company-sales-data-example \
    --server-side-encryption-configuration \
    '{"Rules":[{"ApplyServerSideEncryptionByDefault":{"SSEAlgorithm":"AES256"}}]}'
```

## Enabling S3 Versioning

```text
aws s3api put-bucket-versioning \
    --bucket company-sales-data-example \
    --versioning-configuration Status=Enabled
```

## Blocking Public Access

```text
aws s3api put-public-access-block \
    --bucket company-sales-data-example \
    --public-access-block-configuration \
    "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true"
```

## Connecting to a Database Over an Encrypted Connection

```python
import os
import psycopg2

connection = psycopg2.connect(
    host=os.environ.get("RDS_HOST"),
    database="salesdb",
    user=os.environ.get("RDS_USER"),
    password=os.environ.get("RDS_PASSWORD"),
    sslmode="require"
)
```

Setting `sslmode` to `require` enforces encryption in transit.

## A Security Checklist

1. Enable multi factor authentication on all privileged accounts.
2. Restrict security groups to specific ports and addresses.
3. Enable encryption at rest on storage and databases.
4. Enforce encrypted connections in transit.
5. Block public access on buckets unless there is a deliberate need.
6. Enable logging and review it periodically.
7. Remove permissions and credentials that are no longer needed.