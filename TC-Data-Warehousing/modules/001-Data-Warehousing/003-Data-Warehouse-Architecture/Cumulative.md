<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Describe the typical layers of a data warehouse architecture.
- Explain the role of the staging area, storage layer, and presentation layer.
- Differentiate between single tier, two tier, and three tier data warehouse architectures.
- Identify where a data pipeline fits within the overall architecture.
- Recognize common components used to access and analyze warehouse data.

</details>

<details><summary>Description</summary>

## The General Flow

A data warehouse is not a single piece of software. It is a layered system that data moves through, from its original source to the reports and dashboards that business users ultimately see. Understanding the layers makes it easier to reason about where a problem or a new requirement fits.

At a high level, data moves through three stages:

```text
Source Systems
     ↓
Staging Area
     ↓
Data Warehouse Storage
     ↓
Presentation / Access Layer
```

---

## Source Systems

These are the original systems that generate data in the first place: an ordering application, a customer relationship management tool, a point of sale system, external data feeds, and so on. The warehouse does not modify these systems. It reads from them, typically on a schedule.

---

## Staging Area

The staging area is a temporary holding space where raw data lands after being pulled from source systems, before it is transformed and loaded into the warehouse proper. This separation matters for a few reasons:

- It isolates the warehouse from any inconsistencies or errors in the raw source data.
- It allows data from very different systems to be cleaned and standardized before being combined.
- It gives a natural checkpoint to validate data before it becomes part of the permanent historical record.

Data in the staging area is usually short lived and is cleared out once it has been successfully processed into the warehouse.

---

## Data Warehouse Storage

This is the core of the system, where cleaned, integrated, historical data actually lives. It is structured for efficient querying and analysis rather than for the fast, small transactions an operational database handles. This is also where the data modeling concepts covered later, such as fact and dimension tables, come into play.

---

## Presentation and Access Layer

This is how end users and analysts actually interact with the warehouse. It commonly includes:

- Business intelligence tools that connect directly to the warehouse for dashboards and reports.
- Data marts, which are smaller, more focused subsets of the warehouse built for a specific department, such as finance or marketing.
- Direct SQL access for analysts writing custom queries.

---

## Single Tier, Two Tier, and Three Tier Architectures

Data warehouse architectures are often categorized by how many distinct layers separate the source data from the end user.

- **Single Tier**: Minimizes the amount of data stored separately from source systems. Rarely used in practice due to performance and separation concerns.
- **Two Tier**: Separates source systems from the warehouse, but does not include a distinct staging or presentation layer. Simpler, but less flexible.
- **Three Tier**: The most common approach, consisting of the source system layer, the data warehouse layer including staging, and the presentation or analysis layer. This is the structure described above, and the one most production systems follow.

</details>

<details><summary>Real World Application</summary>

## Where Engineers Actually Work in This Architecture

A data engineer's day to day work is usually concentrated in the movement between layers, building and maintaining the process that pulls data from source systems into staging, then transforms and loads it into the warehouse. This process is commonly referred to as a data pipeline, and it is the practical implementation of the arrows in the architecture diagram above. Business analysts and report builders, by contrast, mostly interact with the presentation layer and rarely need to know the details of how data got there.

</details>

<details><summary>Implementation</summary>

## Setting Up the Layers

A three tier architecture is typically implemented as separate schemas or databases, keeping each layer isolated.

```sql
CREATE SCHEMA staging;
CREATE SCHEMA warehouse;
CREATE SCHEMA reporting;
```

## Staging Table Example

Staging tables usually accept data loosely, using text columns, so that a malformed value does not cause the load to fail before it can be inspected.

```sql
CREATE TABLE staging.raw_orders (
    order_id      VARCHAR(50),
    customer_id   VARCHAR(50),
    order_date    VARCHAR(50),
    amount        VARCHAR(50),
    loaded_at     TIMESTAMP
);
```

## Warehouse Table Example

The warehouse layer enforces proper data types, after validation has occurred.

```sql
CREATE TABLE warehouse.orders (
    order_id      INT PRIMARY KEY,
    customer_id   INT,
    order_date    DATE,
    amount        DECIMAL(10, 2)
);
```

## Moving Data Between Layers

```sql
INSERT INTO warehouse.orders (order_id, customer_id, order_date, amount)
SELECT
    CAST(order_id AS INT),
    CAST(customer_id AS INT),
    CAST(order_date AS DATE),
    CAST(amount AS DECIMAL(10, 2))
FROM staging.raw_orders
WHERE order_id IS NOT NULL
  AND amount IS NOT NULL;
```

## Steps to Follow

1. Create separate schemas for staging, warehouse, and reporting.
2. Load raw source data into staging with permissive column types.
3. Validate and filter the staged data.
4. Cast values to proper types and insert into warehouse tables.
5. Clear the staging tables once the load has succeeded.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Data warehouse architecture is a layered flow from source systems to a presentation layer.
- The staging area holds raw data temporarily before it is cleaned and loaded into the warehouse.
- The warehouse storage layer holds cleaned, integrated, historical data structured for analysis.
- The presentation layer includes business intelligence tools, data marts, and direct query access.
- Three tier architecture, separating source, warehouse, and presentation layers, is the most common approach used in practice.

This layered structure sets up the next topic, which looks at the different vendors and platforms that implement these layers in practice.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
