## Two Different Philosophies for Storing Large Data

A data warehouse, as covered earlier, stores structured, cleaned, integrated data, organized specifically to support business analysis. A data lake takes a different approach: it stores data in its raw, original form, structured or not, and defers the work of cleaning and organizing it until later, only when that data is actually going to be used.

---

## Structure and Format

A data warehouse requires data to be transformed into a defined structure before it is loaded, following the fact and dimension modeling approach covered in later modules. This is often called schema on write, since the structure is defined before the data is written into the system.

A data lake accepts data in almost any format: structured tables, semi structured formats like JSON, and fully unstructured data like images, audio, or raw log files. The structure is only applied later, at the point the data is read and used. This is called schema on read.

```text
Data Warehouse:  Data → Transform → Structured Storage → Query
Data Lake:       Data → Store As Is → Structure Applied When Queried
```

---

## Cost and Storage

Data lakes are typically built on low cost storage systems, such as Amazon S3, covered later in this section, which makes storing very large volumes of raw data economically practical. Data warehouses generally cost more per unit of storage, since that cost also covers the structure, indexing, and query performance the warehouse provides.

This often leads organizations to store all of their raw data cheaply in a data lake first, and only move the specific, cleaned subset of that data that is actually needed for regular business reporting into a data warehouse.

---

## Comparing the Two Approaches

| | Data Warehouse | Data Lake |
|---|---|---|
| Data format | Structured only | Structured, semi structured, and unstructured |
| Schema | Defined before loading (schema on write) | Applied when read (schema on read) |
| Cost | Higher per unit stored | Lower per unit stored |
| Primary users | Business analysts, reporting tools | Data scientists, data engineers |
| Typical use | Regular business reporting and dashboards | Exploratory analysis, machine learning, raw data archival |

---

## The Data Lakehouse

A more recent approach, known as a data lakehouse, attempts to combine the low cost, flexible storage of a data lake with the structure and query performance of a data warehouse. This is achieved through additional tooling layered on top of lake storage that adds warehouse like features, such as enforced structure and faster queries, without requiring data to be fully duplicated into a separate warehouse system. This approach is becoming increasingly common, though the underlying distinction between the raw, flexible nature of a lake and the structured, curated nature of a warehouse remains useful to understand regardless of which specific tooling an organization uses.