<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Identify major cloud based data warehouse platforms in current use.
- Describe key differences between Snowflake, Amazon Redshift, and Google BigQuery at a high level.
- Explain the general shift from on premises warehouses to cloud based warehouses.
- Recognize how pricing models differ across major platforms.
- Understand that platform choice depends on an organization's existing infrastructure and needs.

</details>

<details><summary>Description</summary>

## From On Premises to the Cloud

Earlier data warehouses were typically built and run on hardware an organization owned and maintained directly. This required significant upfront investment and ongoing maintenance, and scaling up meant purchasing more physical hardware.

Most modern data warehouses are now cloud based, meaning they run on infrastructure managed by a third party provider, and organizations pay based on usage rather than owning hardware outright. This shift has made warehousing accessible to organizations of nearly any size, since there is no longer a large upfront hardware cost to get started.

---

## Snowflake

Snowflake is a cloud native data warehouse platform, built from the ground up to run in the cloud rather than adapted from an older on premises product. Its most distinctive design choice is separating storage and compute, meaning the space used to store data and the processing power used to query it can scale independently of each other. This allows multiple teams to run queries at the same time without competing for the same resources.

Snowflake runs on top of major cloud providers such as AWS, Azure, and Google Cloud, rather than being tied to just one.

---

## Amazon Redshift

Redshift is Amazon Web Services' data warehouse offering, tightly integrated with the rest of the AWS ecosystem, including services such as S3 for storage and IAM for access control, both covered later in this section. It is a common choice for organizations that are already heavily invested in AWS infrastructure, since it connects easily with other AWS services they are likely already using.

Redshift uses a column oriented storage model, which is well suited to the kind of large scale aggregate queries common in analytical workloads.

---

## Google BigQuery

BigQuery is Google Cloud's data warehouse platform, notable for its serverless design. Rather than provisioning and managing servers or clusters directly, users simply run queries, and BigQuery handles the underlying infrastructure automatically. Pricing is often based on the amount of data scanned by a query, rather than on server time.

BigQuery integrates closely with other Google Cloud tools and is a common choice for organizations already using the Google Cloud ecosystem.

---

## Comparing the Three at a High Level

| | Snowflake | Redshift | BigQuery |
|---|---|---|---|
| Cloud provider | Runs on AWS, Azure, or GCP | AWS only | Google Cloud only |
| Architecture | Separates storage and compute | Cluster based | Fully serverless |
| Common pricing model | Compute time and storage used | Cluster size and time running | Data scanned per query |
| Typical fit | Multi cloud or cloud agnostic organizations | Organizations already using AWS | Organizations already using Google Cloud |

The right platform for a given organization usually depends less on which one is technically superior, and more on which cloud ecosystem the organization already uses, and what its existing team is familiar with.

</details>

<details><summary>Real World Application</summary>

## Vendor Choice in Practice

A company already running its applications on AWS is likely to choose Redshift, since it avoids the added complexity of managing data across cloud providers and takes advantage of existing AWS billing and security setup. A company that operates across multiple cloud providers, or that wants to avoid being tied to any single one, might choose Snowflake specifically because of its cloud agnostic design. These decisions are typically made once, early in a project, since migrating a data warehouse to a different platform later is a significant undertaking.

</details>

<details><summary>Implementation</summary>

## Evaluating a Platform

A structured comparison usually covers the same categories for each candidate platform.

1. Which cloud provider is the organization already using?
2. What is the expected data volume, and how quickly will it grow?
3. How many concurrent users will query the warehouse?
4. What is the team's existing SQL and platform experience?
5. How does the pricing model align with expected usage patterns?

## Connecting to a Warehouse from Python

The connection pattern is similar across platforms, differing mainly in the connector library used.

```python
# Example connection pattern using environment variables
import os

config = {
    "account":   os.environ.get("WAREHOUSE_ACCOUNT"),
    "user":      os.environ.get("WAREHOUSE_USER"),
    "password":  os.environ.get("WAREHOUSE_PASSWORD"),
    "database":  "sales_warehouse",
    "schema":    "public"
}
```

Credentials are read from environment variables rather than written directly into the code.

## Running a Query

```python
def run_query(connection, sql):
    cursor = connection.cursor()
    cursor.execute(sql)
    rows = cursor.fetchall()
    cursor.close()
    return rows
```

## Cost Awareness

Because several platforms bill based on data scanned, limiting the columns and rows a query touches has a direct cost effect.

```sql
-- Scans every column
SELECT * FROM warehouse.orders;

-- Scans only what is needed
SELECT order_id, amount
FROM warehouse.orders
WHERE order_date >= '2024-01-01';
```

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Most modern data warehouses run in the cloud rather than on organization owned hardware.
- Snowflake separates storage and compute and runs across multiple cloud providers.
- Amazon Redshift integrates tightly with the AWS ecosystem and uses column oriented storage.
- Google BigQuery is fully serverless and commonly priced by the amount of data scanned per query.
- Platform choice is typically driven by an organization's existing cloud ecosystem rather than by one platform being universally best.

Understanding the platform landscape sets up the next topic, which looks at how the type of workload itself, transactional versus analytical, shapes which kind of system is appropriate in the first place.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
