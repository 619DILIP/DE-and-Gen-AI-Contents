<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Describe the structure of a star schema.
- Describe the structure of a snowflake schema and how it differs from a star schema.
- Explain the tradeoffs between the two approaches.
- Read a schema diagram and identify the fact table and dimension tables within it.
- Choose an appropriate schema design for a given scenario.

</details>

<details><summary>Description</summary>

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

</details>

<details><summary>Real World Application</summary>

## Designing a Schema for a New Reporting Need

When a business team requests a new report, a data engineer typically starts by identifying the grain of the fact table needed to answer that report's questions, then works backward to determine which dimensions provide the necessary context. For most standard business reporting, such as sales, orders, or website traffic, a star schema is the default starting point, since it keeps the resulting queries simple enough for business intelligence tools and analysts to work with directly, without requiring deep SQL expertise to write multi table joins.

</details>

<details><summary>Implementation</summary>

## Building a Star Schema

In a star schema, each dimension is one flat table containing all its attributes.

```sql
CREATE TABLE dim_product (
    product_id    INT PRIMARY KEY,
    product_name  VARCHAR(100),
    category      VARCHAR(50),
    subcategory   VARCHAR(50),
    brand         VARCHAR(50)
);
```

Querying requires a single join.

```sql
SELECT
    p.category,
    SUM(f.revenue) AS revenue
FROM fact_sales f
JOIN dim_product p ON f.product_id = p.product_id
GROUP BY p.category;
```

## Building a Snowflake Schema

The same dimension normalized into separate tables.

```sql
CREATE TABLE dim_category (
    category_id   INT PRIMARY KEY,
    category_name VARCHAR(50)
);

CREATE TABLE dim_brand (
    brand_id   INT PRIMARY KEY,
    brand_name VARCHAR(50)
);

CREATE TABLE dim_product (
    product_id   INT PRIMARY KEY,
    product_name VARCHAR(100),
    category_id  INT REFERENCES dim_category(category_id),
    brand_id     INT REFERENCES dim_brand(brand_id)
);
```

Querying now requires an extra join.

```sql
SELECT
    c.category_name,
    SUM(f.revenue) AS revenue
FROM fact_sales f
JOIN dim_product p  ON f.product_id = p.product_id
JOIN dim_category c ON p.category_id = c.category_id
GROUP BY c.category_name;
```

## Steps to Follow

1. Start with the fact table and its defined grain.
2. List the dimensions that provide context for that fact.
3. Default to a star schema, keeping each dimension flat.
4. Normalize a dimension only if it is large and highly repetitive.
5. Confirm that common business queries remain simple to write.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- A star schema connects a fact table to fully denormalized, flat dimension tables.
- A snowflake schema normalizes dimension tables into related tables to reduce redundancy.
- Star schemas generally offer simpler, faster queries, while snowflake schemas save storage space.
- The choice between them depends on the size of the dimensions and how much query performance matters relative to storage.
- Star schemas are the more common default in modern data warehouse design.

With schema design covered, the next topic shifts from how data is structured once it arrives in the warehouse to how it gets there in the first place, through ETL and ELT processes.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
