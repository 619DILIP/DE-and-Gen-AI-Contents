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