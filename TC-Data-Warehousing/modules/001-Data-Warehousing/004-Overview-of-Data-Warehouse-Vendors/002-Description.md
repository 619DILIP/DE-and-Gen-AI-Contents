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