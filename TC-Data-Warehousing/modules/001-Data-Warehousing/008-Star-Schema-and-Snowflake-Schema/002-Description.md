## Arranging Facts and Dimensions

With fact and dimension tables defined, the next step is arranging them into a complete schema. The two most common patterns for doing this are the star schema and the snowflake schema. Both use the same underlying fact and dimension concepts, and they differ mainly in how the dimension tables themselves are structured.

---

## Star Schema

In a star schema, one central fact table connects directly to a set of dimension tables, each of which is fully denormalized, meaning all of its descriptive attributes are stored flat in a single table rather than split across multiple related tables. When diagrammed, the fact table sits in the middle with dimension tables branching outward around it, resembling a star.

```text
                Dim_Customer
                     |
Dim_Date  ---   Fact_Sales   ---  Dim_Product
                     |
                Dim_Store
```

For example, `Dim_Product` in a star schema would include every relevant product attribute, product name, category, and brand, directly in one table, even if category and brand information could theoretically be broken out into their own separate tables.

Star schemas are the more common design in practice because their simplicity keeps queries fast. Fewer joins are needed to answer a question, since each dimension is already flat.

---

## Snowflake Schema

A snowflake schema takes the same overall structure but normalizes the dimension tables, splitting them into multiple related tables to reduce redundancy. Continuing the product example, `Dim_Product` might be split so that category information lives in its own separate `Dim_Category` table, referenced by a foreign key.

```text
Dim_Category
     |
Dim_Product   ---   Fact_Sales   ---   Dim_Customer
                         |
                     Dim_Date
```

This is called a snowflake schema because the branching, normalized dimension tables resemble the arms of a snowflake extending outward from the central fact table.

---

## Comparing the Two

| | Star Schema | Snowflake Schema |
|---|---|---|
| Dimension structure | Denormalized, flat | Normalized, split into related tables |
| Query complexity | Fewer joins, simpler queries | More joins, more complex queries |
| Storage redundancy | More repeated data across rows | Less redundant data |
| Query performance | Generally faster | Generally slower due to extra joins |
| Common usage | Most common in modern data warehouses | Used when storage efficiency matters more than query speed |

---

## Choosing Between Them

In most modern data warehouses, storage is relatively inexpensive compared to the cost of slow queries, so the star schema's simplicity and query performance usually outweigh the storage savings a snowflake schema would provide. Snowflake schemas are more often chosen in situations where dimension tables are extremely large and repeated data would create a meaningful storage or maintenance burden, or where an organization already has a normalized data model it wants to preserve.
