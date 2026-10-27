## A Complete Function

Bringing together the S3 trigger, transformation, and database write.

```python
import json
import os
import boto3
import psycopg2

s3 = boto3.client("s3")

def get_connection():
    return psycopg2.connect(
        host=os.environ["DB_HOST"],
        database=os.environ["DB_NAME"],
        user=os.environ["DB_USER"],
        password=os.environ["DB_PASSWORD"],
    )

def transform(rows):
    cleaned = []
    for row in rows:
        if not row.get("order_id") or not row.get("amount"):
            continue
        cleaned.append((
            int(row["order_id"]),
            float(row["amount"]),
            row["region"].strip().upper(),
        ))
    return cleaned

def lambda_handler(event, context):
    processed = 0

    for record in event["Records"]:
        bucket = record["s3"]["bucket"]["name"]
        key = record["s3"]["object"]["key"]
        print(f"Processing {key} from {bucket}")

        # Extract
        obj = s3.get_object(Bucket=bucket, Key=key)
        rows = json.loads(obj["Body"].read().decode("utf-8"))

        # Transform
        clean = transform(rows)
        skipped = len(rows) - len(clean)
        if skipped:
            print(f"Skipped {skipped} invalid rows in {key}")

        # Load
        conn = get_connection()
        cursor = conn.cursor()
        cursor.executemany(
            "INSERT INTO orders (order_id, amount, region) VALUES (%s, %s, %s)",
            clean,
        )
        conn.commit()
        cursor.close()
        conn.close()

        processed += len(clean)

    return {"statusCode": 200, "body": f"Inserted {processed} rows"}
```

Several practices from earlier modules appear. Credentials come from environment variables rather than the code. The SQL uses parameter placeholders. Invalid rows are skipped and logged rather than failing the whole invocation. And the loop over `event["Records"]` handles multiple objects rather than assuming one.

---

## The Execution Role Policy

The permissions the function needs, and nothing further.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::partner-uploads/*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "logs:CreateLogGroup",
                "logs:CreateLogStream",
                "logs:PutLogEvents"
            ],
            "Resource": "*"
        }
    ]
}
```

Reading is granted on one specific bucket. There is no delete permission, no access to other buckets, and no broader S3 access.

---

## Creating a Function from the Command Line

Packaging and deploying, using the same CLI covered earlier.

```text
# Package the code
zip function.zip lambda_function.py

# Create the function
aws lambda create-function \
    --function-name process-partner-uploads \
    --runtime python3.12 \
    --handler lambda_function.lambda_handler \
    --role arn:aws:iam::000000000000:role/lambda-pipeline-role \
    --zip-file fileb://function.zip

# List functions
aws lambda list-functions
```

---

## Invoking and Testing

A function can be invoked directly, without waiting for a real event, by supplying a test event.

```text
# A minimal S3 event, saved as test-event.json
aws lambda invoke \
    --function-name process-partner-uploads \
    --payload file://test-event.json \
    response.json

cat response.json
```

```json
{
  "Records": [
    {
      "s3": {
        "bucket": { "name": "partner-uploads" },
        "object": { "key": "acme/orders-2024-06-01.json" }
      }
    }
  ]
}
```

Testing with a constructed event like this is standard practice, since it exercises the function without needing to upload a real file each time.

---

## Connecting the S3 Trigger

```text
aws s3api put-bucket-notification-configuration \
    --bucket partner-uploads \
    --notification-configuration file://notification.json
```

```json
{
  "LambdaFunctionConfigurations": [
    {
      "LambdaFunctionArn": "arn:aws:lambda:us-east-1:000000000000:function:process-partner-uploads",
      "Events": ["s3:ObjectCreated:*"]
    }
  ]
}
```

Once configured, any object created in the bucket invokes the function automatically.

---

## Setting Environment Variables

```text
aws lambda update-function-configuration \
    --function-name process-partner-uploads \
    --environment "Variables={DB_HOST=db.internal,DB_NAME=sales,DB_USER=pipeline}"
```

Values genuinely sensitive, such as a database password, are better held in a dedicated secrets service and retrieved at runtime, rather than stored as plain environment variables.

---

## Steps to Follow

1. Write the handler function, accepting `event` and `context`.
2. Define an execution role granting only the permissions the function needs, including log writing.
3. Package the code and create the function, specifying the runtime and handler path.
4. Set configuration values as environment variables rather than hardcoding them.
5. Test by invoking directly with a constructed event before wiring up a real trigger.
6. Attach the trigger, such as an S3 bucket notification.
7. Check the logs after the first real invocation to confirm the expected behavior.