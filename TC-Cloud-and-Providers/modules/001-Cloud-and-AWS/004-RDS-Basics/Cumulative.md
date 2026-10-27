<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Define Amazon RDS and explain what problem it solves.
- Identify the database engines supported by RDS.
- Explain what "managed" means in the context of a managed database service.
- Describe common RDS features such as automated backups and read replicas.
- Recognize how an application connects to an RDS database.

> **Before you start**
>
> This module walks through the process so you understand how the service works and what the steps involve. **You do not need to do any of this hands on right now, and you should not create a personal AWS account to follow along.**
>
> Hands on practice comes later this week, once the Floci module introduces a local environment where you can run all of these commands safely, at no cost, without an AWS account. Read through the steps here, then apply them there.

</details>

<details><summary>Description</summary>

## What Is RDS?

Amazon Relational Database Service, known as RDS, is a managed database service that allows a relational database to be launched and run in AWS without needing to manually install, configure, and maintain the underlying database software or server.

The SQL concepts covered earlier in this curriculum, tables, queries, joins, and constraints, all still apply directly on an RDS database. RDS does not change how SQL works. It changes how the database server itself is provisioned and maintained.

---

## Running a Database Without RDS

Before managed services like RDS existed, running a relational database required manually installing database software on a server, such as an EC2 instance, and then handling ongoing maintenance tasks directly: applying security patches, configuring backups, monitoring performance, and managing failover if the server went down.

---

## What RDS Manages Automatically

RDS handles much of this maintenance automatically:

- **Software installation and patching**: The underlying database engine is installed and kept up to date automatically.
- **Automated backups**: RDS can take regular, automatic backups of the database, allowing it to be restored to an earlier point in time if needed.
- **Monitoring**: Built in monitoring tracks database performance and resource usage.
- **Read replicas**: RDS can create additional read only copies of a database, allowing read heavy applications to distribute query load across multiple copies rather than a single database instance.

This is what "managed" means in this context: AWS handles the operational overhead of keeping the database running reliably, so that developers and data engineers can focus on the data and queries themselves.

---

## Supported Database Engines

RDS supports several common relational database engines, including MySQL, PostgreSQL, and Microsoft SQL Server, among others. The choice of engine typically depends on what an application or team already uses, since the underlying SQL syntax and behavior differ slightly between engines, consistent with what was covered in earlier SQL modules regarding dialect differences.

---

## Connecting to RDS

An application, or an EC2 instance running a data pipeline, connects to an RDS database over the network using a connection string, which includes the database's endpoint address, port, and login credentials. From the perspective of the application code, this connection behaves the same way as connecting to any other relational database, using the same Python database libraries covered in earlier modules for connecting Python to SQL.

```text
Application / EC2 Instance  →  Network Connection  →  RDS Database Endpoint
```

</details>

<details><summary>Real World Application</summary>

## RDS Inside a Data Pipeline

A data pipeline, whether running on a scheduled EC2 instance or as an event driven Lambda function, commonly reads raw source data, transforms it, and writes the finished result into an RDS database acting as a staging or warehouse layer. Because RDS handles backups and patching automatically, the team building the pipeline can focus on the transformation logic itself, rather than spending time on database server maintenance. If the pipeline needs to support many simultaneous analytical queries without slowing down, a read replica can be added so those queries run against a separate copy of the database, without affecting the primary database receiving new pipeline data.

</details>

<details><summary>Implementation</summary>

## Creating a Database Instance

1. Open the RDS service in the AWS Management Console.
2. Select a database engine, such as PostgreSQL or MySQL.
3. Choose an instance size appropriate to the expected workload.
4. Set a master username and a strong password.
5. Configure network access so only trusted sources can reach the database.
6. Enable automated backups and set a retention period.

## Finding the Connection Endpoint

Once the instance is available, the console displays an endpoint address used for connections.

```text
mydb.abc123xyz.us-east-1.rds.amazonaws.com
```

## Connecting from Python

```python
import os
import psycopg2

connection = psycopg2.connect(
    host=os.environ.get("RDS_HOST"),
    port=5432,
    database="salesdb",
    user=os.environ.get("RDS_USER"),
    password=os.environ.get("RDS_PASSWORD")
)

cursor = connection.cursor()
cursor.execute("SELECT COUNT(*) FROM orders;")
print(cursor.fetchone())

cursor.close()
connection.close()
```

Credentials are read from environment variables rather than written into the code.

## Creating a Table

```python
cursor = connection.cursor()
cursor.execute("""
    CREATE TABLE IF NOT EXISTS orders (
        order_id    INT PRIMARY KEY,
        customer_id INT,
        order_date  DATE,
        amount      DECIMAL(10, 2)
    )
""")
connection.commit()
```

## Steps to Follow

1. Create the RDS instance with an appropriate engine and size.
2. Restrict network access to specific trusted sources.
3. Store the connection credentials outside of application code.
4. Test the connection before writing pipeline logic against it.
5. Confirm automated backups are enabled and retained appropriately.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- RDS is a managed relational database service that removes the need to manually maintain database server software.
- RDS automatically handles patching, backups, and monitoring.
- Read replicas allow read heavy workloads to be distributed across multiple copies of a database.
- RDS supports common engines such as MySQL, PostgreSQL, and SQL Server.
- Applications connect to RDS the same way they would connect to any relational database, using standard connection details and libraries.

With compute and database services covered, the next module looks at Amazon S3, the storage service commonly used for raw data and data lake style storage.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>