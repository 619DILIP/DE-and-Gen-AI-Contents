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