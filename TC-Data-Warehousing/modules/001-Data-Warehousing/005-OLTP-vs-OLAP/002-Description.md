## Two Very Different Jobs

Databases exist to serve very different purposes depending on what they are used for. OLTP and OLAP describe two broad categories of database workload, and understanding the difference explains why organizations often run separate systems for their day to day operations and their reporting and analysis.

---

## OLTP: Online Transaction Processing

OLTP systems are designed to handle a high volume of short, simple transactions in real time. Examples include placing an order, updating a bank balance, or checking a customer into a hotel. These systems prioritize:

- Speed for individual, small operations.
- Accuracy and consistency, since these transactions often involve money or inventory.
- Support for many simultaneous users performing different operations at once.

A typical OLTP query touches a small number of rows, for example fetching a single customer's record or updating one order's status. The database structure behind an OLTP system, covered in earlier SQL modules through concepts like normalization, is designed to avoid duplicate data and support fast, precise updates.

---

## OLAP: Online Analytical Processing

OLAP systems are designed for the opposite kind of workload: large scale queries that aggregate and analyze data across many records, often spanning long periods of time. Examples include calculating total revenue by region over the past year, or identifying the best selling product category across every store.

OLAP systems prioritize:

- Fast performance on queries that scan large volumes of historical data.
- Support for complex aggregation, filtering, and grouping.
- Read heavy access patterns, since OLAP systems are queried far more often than they are updated.

A data warehouse is a form of OLAP system. The data modeling approaches used in warehousing, such as star schemas, exist specifically to make this kind of large scale aggregate query fast.

---

## Comparing OLTP and OLAP

| | OLTP | OLAP |
|---|---|---|
| Purpose | Run day to day operations | Support analysis and reporting |
| Query type | Small, simple, frequent | Large, complex, less frequent |
| Data volume touched per query | Few rows | Many rows, often millions |
| Data structure | Normalized, minimizes redundancy | Denormalized, optimized for read performance |
| Users | Applications, front line staff | Analysts, decision makers |
| Update frequency | Constant, real time | Periodic, in batches |

---

## Why Not Use One System for Both?

It is technically possible to run analytical queries directly against an OLTP system, but doing so at scale creates problems. Large, complex OLAP style queries can consume enough resources to slow down the very transactions the OLTP system exists to process quickly. This is one of the central reasons organizations maintain a separate data warehouse: it allows analytical workloads to run without any risk of degrading the performance of live operational systems.
