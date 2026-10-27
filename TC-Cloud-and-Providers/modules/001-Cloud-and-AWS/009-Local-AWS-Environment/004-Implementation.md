## Full Setup, Step by Step

1. Confirm Docker is installed and running with `docker --version`.
2. Confirm the AWS CLI is installed with `aws --version`.
3. Create a `compose.yaml` file with the Floci service definition.
4. Start the emulator with `docker compose up`.
5. Set the four environment variables in the terminal that will be used for work.
6. Verify with `aws s3 mb s3://test-bucket` followed by `aws s3 ls`.

---

## Working Through the Earlier Modules Locally

The commands from the earlier AWS modules can now be run directly. For example, from the S3 module:

```text
aws s3 mb s3://company-sales-data-example
aws s3 cp orders.csv s3://company-sales-data-example/raw/orders.csv
aws s3 ls s3://company-sales-data-example/raw/
```

From the Cloud Security module:

```text
aws s3api put-bucket-versioning \
    --bucket company-sales-data-example \
    --versioning-configuration Status=Enabled
```

From the IAM module:

```text
aws iam create-role \
    --role-name pipeline-s3-read-role \
    --assume-role-policy-document file://trust-policy.json

aws iam list-roles
```

None of these commands differ from their real AWS equivalents. Only the endpoint they are sent to has changed.

---

## Stopping and Resetting

Stopping the emulator releases the resources it was using.

```text
docker compose down
```

By default, everything created inside Floci is discarded when the container stops. Starting again gives a clean environment. This is useful when an exercise goes wrong, since starting over costs nothing.

---

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| Connection refused | Floci is not running | Check `docker compose up` is active |
| Commands hit real AWS | Endpoint variable not set | Re-export the variables in the current terminal |
| Credential errors | Variables missing | Set placeholder access key and secret |
| Port already in use | Something else is on 4566 | Stop the other process, or map a different port |
| Resources missing after restart | Data is not persisted by default | Expected behavior; recreate them |

---

## A Working Check

Running this short script confirms the whole setup end to end.

```python
import boto3

s3 = boto3.client(
    "s3",
    endpoint_url="http://localhost:4566",
    region_name="us-east-1",
    aws_access_key_id="test",
    aws_secret_access_key="test",
)

s3.create_bucket(Bucket="verify-bucket")
s3.put_object(Bucket="verify-bucket", Key="hello.txt", Body=b"working")

obj = s3.get_object(Bucket="verify-bucket", Key="hello.txt")
print(obj["Body"].read().decode())
```

Output of `working` confirms that creating a bucket, writing an object, and reading it back all function correctly.