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