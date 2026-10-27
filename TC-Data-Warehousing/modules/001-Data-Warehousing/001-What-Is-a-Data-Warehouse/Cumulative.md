<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Define a data warehouse in plain terms.
- Explain the purpose a data warehouse serves within an organization.
- Identify the kinds of data typically stored in a data warehouse.
- Describe how a data warehouse differs from a standard operational database.
- Recognize common examples of data warehouse use.

</details>

<details><summary>Description</summary>

## Defining a Data Warehouse

A data warehouse is a centralized system that stores large volumes of data collected from multiple sources across an organization, structured specifically to support reporting and analysis. Rather than running the day to day operations of a business, a data warehouse exists to answer questions about that business over time.

A retail company, for example, might have separate systems handling online orders, in store sales, inventory, and customer support. A data warehouse pulls relevant data from each of these systems into one place, so that a single query can answer a question like "what were total sales across every channel last quarter" without needing to combine data manually from four different systems.

---

## Why Not Just Use the Operational Database?

Every application that runs a business, an ordering system, a website, a point of sale terminal, is backed by a database designed to handle that specific job well. These operational databases are optimized for fast, small transactions: placing an order, updating a customer address, checking inventory for one item.

Running large analytical queries directly against these databases creates two problems:

- **Performance**: A query that scans millions of historical rows to compute a trend can slow down the live system that customers are actively using.
- **Structure**: Operational databases are usually organized around the needs of a single application, not around the kinds of questions a business analyst wants to ask across the whole company.

A data warehouse solves both problems by existing as a separate system, built specifically for large scale historical queries, decoupled from the systems running live operations.

---

## What Kind of Data Lives in a Data Warehouse?

A data warehouse typically holds:

- Historical data, often spanning years, rather than only the current state.
- Data pulled from multiple source systems, combined and standardized into one structure.
- Data organized around business concepts such as sales, customers, or products, rather than around the technical needs of one application.

This is different from an operational database, which usually only needs to know the current state of things, such as a customer's current address, not every address they have ever had.

---

## Key Characteristics

Data warehouses are commonly described using four characteristics, first outlined by Bill Inmon, one of the earliest and most influential figures in data warehousing:

- **Subject Oriented**: Data is organized around business subjects like sales or customers, not around individual applications.
- **Integrated**: Data pulled from different source systems is standardized into a consistent format, so the same customer or product is represented the same way everywhere.
- **Time Variant**: Data reflects change over time, so historical trends can be analyzed, not just the current snapshot.
- **Non Volatile**: Once data is loaded into the warehouse, it is not routinely updated or deleted the way operational data is. It represents a stable historical record.

</details>

<details><summary>Real World Application</summary>

## A Retail Example

Consider a national retail chain with hundreds of stores plus an online storefront. Store transactions live in one system, online orders in another, and customer loyalty data in a third. None of these systems alone can answer a question like "which product categories grew fastest among loyalty members over the past two years, broken down by region."

A data warehouse solves this by regularly pulling data from all three systems, standardizing it, for example making sure a product ID means the same thing everywhere, and storing it in a structure built for exactly this kind of cross system, historical analysis. Business analysts then query the warehouse directly, without needing to understand or access the three original operational systems at all.

</details>

<details><summary>Implementation</summary>

## Identifying Warehouse Requirements

Before building anything, the requirements are usually gathered by answering a set of questions.

1. What business questions need to be answered?
2. Which source systems hold the data required to answer them?
3. How far back does historical data need to go?
4. How frequently does the data need to be refreshed?
5. Who will query the warehouse, and using which tools?

## Mapping Sources to a Warehouse

```text
Source: Online Orders System     ->  order data
Source: In Store POS System      ->  transaction data
Source: Loyalty Program Database ->  customer data
                    |
                    v
            Central Data Warehouse
                    |
                    v
        Reports and Dashboards
```

## A Minimal Warehouse Table

Even a simple warehouse table differs from an operational one by keeping history rather than only current state.

```sql
CREATE TABLE warehouse_sales (
    sale_id        INT,
    customer_id    INT,
    product_id     INT,
    sale_date      DATE,
    quantity       INT,
    revenue        DECIMAL(10, 2),
    source_system  VARCHAR(50),
    loaded_at      TIMESTAMP
);
```

The `source_system` and `loaded_at` columns are common in warehouse tables. They record where each row came from and when it arrived, which supports troubleshooting and auditing.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- A data warehouse is a centralized system built to support reporting and analysis across an organization.
- It differs from an operational database, which is optimized for fast, small, day to day transactions.
- Data warehouses store historical, integrated data pulled from multiple sources.
- The four defining characteristics of a data warehouse are subject oriented, integrated, time variant, and non volatile.
- Data warehouses allow complex, cross system business questions to be answered without impacting live operational systems.

With this foundation in place, the next step is looking at how a data warehouse is actually structured internally.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
