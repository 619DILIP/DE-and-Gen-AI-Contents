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