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