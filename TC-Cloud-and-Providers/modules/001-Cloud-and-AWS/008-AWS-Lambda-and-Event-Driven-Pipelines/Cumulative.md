<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Explain what serverless computing means and how Lambda differs from a server based approach.
- Describe the structure of a Lambda function, including the handler, event, and context.
- Explain how event triggers cause a function to run.
- Describe the execution role a Lambda function needs and why.
- Explain the event driven pipeline pattern connecting S3, Lambda, and a database.
- Compare scheduled and event driven pipelines and identify which suits a given requirement.
- Recognize Lambda's operational limits and cost model.

> **Before you start**
>
> This module walks through the process so you understand how the service works and what the steps involve. **You do not need to do any of this hands on right now, and you should not create a personal AWS account to follow along.**
>
> Hands on practice comes later this week, once the Floci module introduces a local environment where you can run all of these commands safely, at no cost, without an AWS account. Read through the steps here, then apply them there.

</details>

<details><summary>Description</summary>

## From Servers to Functions

Running code on a server means something is always there: an instance is provisioned, an operating system runs, and the machine waits whether or not there is work to do. That model suits work that runs continuously or for long stretches.

A great deal of data work is not like that. A file arrives a few times a day and needs processing. A record changes and something downstream needs updating. Between those moments, nothing needs to happen at all, yet a server sitting idle still costs money and still needs patching and monitoring.

AWS Lambda takes a different approach. Code is uploaded as a function, and AWS runs it in response to an event. There is no server to provision, patch, or shut down. When nothing triggers the function, nothing runs and nothing is billed. This is what the term serverless describes. Servers still exist, but they are entirely managed by AWS and invisible to the person writing the code.

---

## Lambda Compared with EC2

Both run code. The difference is what is being managed and when the code runs.

| | EC2 | Lambda |
|---|---|---|
| Unit of deployment | A virtual machine | A single function |
| What runs | Continuously, until stopped | Only when triggered |
| Billing | For the time the instance is running | Per invocation and execution time |
| Managed by you | OS, patching, scaling, shutdown | Only the function code |
| Suits | Long running or always on workloads | Short, event driven tasks |
| Risk if forgotten | Continues accruing charges | Nothing runs, nothing is billed |

That last row matters practically. An EC2 instance left running after an exercise keeps costing money. A Lambda function left in place costs nothing until something invokes it, which makes it considerably more forgiving for learning.

Neither replaces the other. A nightly job that processes several hours of data is a poor fit for Lambda, which has an execution time limit. A function that runs for two seconds each time a file lands is a poor fit for a dedicated instance.

---

## The Shape of a Lambda Function

A Lambda function is a single function with a specific signature, conventionally called the handler.

```python
def lambda_handler(event, context):
    print("Function invoked")
    return {"statusCode": 200, "body": "Done"}
```

Two arguments are always passed in:

- **event**: a dictionary describing what triggered the function and carrying the relevant details. Its structure depends entirely on the trigger source.
- **context**: information about the invocation itself, such as the remaining execution time and the request ID.

The handler is the entry point. AWS calls it, passes the event, and the function does its work and returns.

---

## Triggers

A Lambda function does nothing until something invokes it. The source of that invocation is the trigger, and the choice of trigger defines how the function fits into a system.

Common triggers include:

- **S3 events**, when an object is created, updated, or deleted in a bucket
- **Scheduled events**, running on a fixed timetable in the way a cron job would
- **API requests**, invoking the function when an HTTP endpoint is called
- **Database or queue events**, when a record changes or a message arrives
- **Direct invocation** from another service or from application code

The S3 trigger is the one most relevant to data work. When a file lands in a bucket, the function runs automatically, receiving details of that file in the event.

```python
def lambda_handler(event, context):
    for record in event["Records"]:
        bucket = record["s3"]["bucket"]["name"]
        key = record["s3"]["object"]["key"]
        print(f"New object: {key} in {bucket}")
    return {"statusCode": 200}
```

The event arrives as a list of records because a single invocation may cover more than one object. Iterating rather than assuming a single file avoids a common bug.

---

## The Execution Role

A Lambda function has no permissions of its own. It assumes an IAM role, called the execution role, which determines what it is allowed to do.

This connects directly to the IAM material covered earlier. A function that reads from one bucket and writes to one database is granted exactly those permissions and nothing more, following the principle of least privilege. No credentials appear anywhere in the function code, because the permissions travel with the role rather than with a stored key.

A typical execution role for a data processing function grants:

- Permission to read objects from the specific source bucket
- Permission to connect to the specific target database
- Permission to write logs, so the function's output is recorded and can be reviewed

That last one is easy to overlook. Without it, the function may run correctly but produce no visible output when something goes wrong, which makes debugging considerably harder.

---

## The Event Driven Pipeline Pattern

This is where the services covered separately in this week come together into one working system.

```text
File lands in S3
      ↓  (S3 event triggers the function)
Lambda function runs
      ↓  (reads the file using its execution role)
Data is validated and transformed
      ↓  (writes using the same role)
Records land in RDS
```

Four things covered as separate modules are doing distinct jobs here. S3 holds the raw file and raises the event. IAM grants the function exactly the access it needs. Lambda runs the transformation. RDS stores the result.

It also implements, in concrete form, the extract, transform, load structure covered in the data warehousing material. The extract is reading the object from S3, the transform is the validation and reshaping in the function body, and the load is the insert into the database.

---

## Scheduled Versus Event Driven

The pipeline material introduced batch pipelines, which run on a schedule, and streaming pipelines, which process data continuously as it arrives. Lambda makes the second of these concrete.

| | Scheduled | Event driven |
|---|---|---|
| Runs | At fixed times | When something happens |
| Typical implementation | An instance running a job on a timer | A function triggered by an event |
| Latency | Up to the length of the interval | Seconds |
| Suits | Predictable volumes, regular reporting | Irregular arrivals, near real time needs |
| Behavior when idle | The schedule still fires | Nothing runs at all |

A nightly warehouse load fits the scheduled model well, since the data is not needed sooner and processing everything at once is efficient. A file that partners upload at unpredictable times fits the event driven model, since waiting until the next scheduled run would add hours of delay for no reason.

Neither is more advanced than the other. They answer different questions about when work needs to happen.

---

## Limits Worth Knowing

Lambda's design imposes constraints that shape what it suits:

- **Execution time** is capped, so long running jobs are not appropriate. Work exceeding the limit needs a different service or needs splitting into smaller pieces.
- **Memory and temporary storage** are allocated per function and bounded, which limits how much data can be held at once.
- **Cold starts** occur when a function has not run recently, adding a short delay while the environment is prepared. Functions invoked frequently avoid this; infrequent ones may notice it.
- **Statelessness** means nothing persists between invocations. Anything that needs to survive must be written to S3, a database, or another external store.

The statelessness point is the one that most often surprises people. Two invocations of the same function share nothing, so a variable set during one run cannot be relied on during the next.

---

## Cost Model

Lambda bills on two dimensions: the number of invocations and the time each one runs, measured against the memory allocated. There is no charge for a function that is deployed but never invoked.

AWS includes a substantial monthly allowance for Lambda at no cost, and unlike time limited introductory offers, this allowance does not expire. For learning and for genuinely low volume workloads, the practical cost is often nothing.

</details>

<details><summary>Real World Application</summary>

## Automating a Partner Data Feed

A company receives sales files from several retail partners, uploaded at unpredictable times throughout the day. Before automation, someone checked for new files each morning and ran a processing script by hand, meaning data was up to a day stale and the process failed silently when that person was away.

Replacing this with an event driven pipeline changes the shape of the problem. Partners upload to an S3 bucket. Each upload triggers a Lambda function that validates the file, standardizes the format differences between partners, and writes the records into the warehouse. Data is available within seconds of arrival, nothing runs when no files are coming in, and there is no server to maintain.

The failure handling also improves. A malformed file from one partner causes that single invocation to fail and be logged, while files from every other partner continue processing normally. Under the previous approach, one bad file could stop the whole morning's run.

</details>

<details><summary>Implementation</summary>

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

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Lambda runs code in response to events without any server to provision or manage.
- A handler function receives an event describing the trigger and a context describing the invocation.
- Triggers determine when a function runs, with S3 object creation being the most relevant to data work.
- An execution role grants the function its permissions, following the principle of least privilege.
- The S3 to Lambda to database pattern connects storage, permissions, compute, and a database into one working pipeline.
- Event driven pipelines complement scheduled ones, suiting irregular arrivals and low latency needs.
- Lambda's execution time limit, statelessness, and cold starts shape which workloads it fits.

This pattern brings together the services covered separately across this week into a single system.

With the services and the pattern that connects them covered, the final module of this section sets up a local environment where all of this can be practiced safely.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
