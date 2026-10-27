<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Define fact tables and dimension tables.
- Explain the concept of grain in a fact table.
- Identify measures and foreign keys within a fact table.
- Identify descriptive attributes within a dimension table.
- Read a simple fact and dimension table structure and explain what it represents.

</details>

<details><summary>Description</summary>

## Two Kinds of Tables

Data warehouses organize data using two distinct types of tables that work together: fact tables and dimension tables. Understanding the difference between them is the foundation for everything else in data warehouse modeling, including the star schema covered in the next module.

---

## Fact Tables

A fact table stores the measurable, numeric events of a business, the things being tracked and analyzed. Each row in a fact table typically represents one occurrence of a business event, such as one sale, one shipment, or one website visit.

A fact table generally contains two kinds of columns:

- **Measures**: numeric values that can be aggregated, such as quantity sold, revenue, or duration.
- **Foreign keys**: references to related dimension tables, which provide the context for that measurement.

```text
Fact_Sales
--------------------------------------------------
sale_id | customer_id | product_id | date_id | quantity | revenue
--------------------------------------------------
1001    | 501         | 20         | 3001    | 2        | 39.98
1002    | 502         | 45         | 3001    | 1        | 12.50
```

Here, `quantity` and `revenue` are measures, while `customer_id`, `product_id`, and `date_id` are foreign keys pointing to dimension tables.

---

## Grain

The grain of a fact table describes exactly what one row represents. This is one of the most important decisions in designing a fact table, since every measure in the table must be consistent with that grain.

In the example above, the grain is one row per individual sale line item. If the grain were instead one row per day per product, the table would need to be restructured to hold total daily quantities and revenue rather than individual transactions. Defining the grain clearly before building a fact table prevents inconsistent or misleading aggregations later.

---

## Dimension Tables

A dimension table stores the descriptive context around a fact, the who, what, where, and when. Dimension tables are generally not numeric in the same way fact tables are. Instead, they contain attributes that describe an entity.

```text
Dim_Customer
--------------------------------------------------
customer_id | customer_name | region  | signup_date
--------------------------------------------------
501         | Maria Chen    | West    | 2022-01-15
502         | James Patel   | East    | 2023-06-02
```

```text
Dim_Product
--------------------------------------------------
product_id | product_name     | category
--------------------------------------------------
20         | Wireless Mouse   | Electronics
45         | Notebook, Ruled  | Office Supplies
```

A dimension table like `Dim_Customer` allows an analyst to answer questions such as "which region generated the most revenue" by joining the fact table to the dimension table on `customer_id`, rather than repeating region information on every single row of the fact table.

---

## Why Separate Facts from Dimensions?

Keeping numeric events and descriptive context in separate tables avoids repeating the same descriptive data across millions of fact rows. In the example above, a customer's name and region are stored once in `Dim_Customer`, not duplicated on every sale that customer makes. This keeps the fact table smaller and faster to query, while dimension tables remain small enough to update easily when descriptive details change.

</details>

<details><summary>Real World Application</summary>

## Answering a Business Question

Consider the question "what was total revenue by product category last month." Answering this requires joining `Fact_Sales` to `Dim_Product` on `product_id`, filtering the fact table's date range, and summing the `revenue` measure grouped by the `category` column from the dimension table.

This pattern, joining a fact table to one or more dimension tables to add context before aggregating, is the single most common type of query run against a data warehouse. It is the direct reason fact and dimension tables are structured the way they are.

</details>

<details><summary>Implementation</summary>

## Creating Dimension Tables

```sql
CREATE TABLE dim_customer (
    customer_id    INT PRIMARY KEY,
    customer_name  VARCHAR(100),
    region         VARCHAR(50),
    signup_date    DATE
);

CREATE TABLE dim_product (
    product_id    INT PRIMARY KEY,
    product_name  VARCHAR(100),
    category      VARCHAR(50),
    brand         VARCHAR(50)
);

CREATE TABLE dim_date (
    date_id     INT PRIMARY KEY,
    full_date   DATE,
    day_of_week VARCHAR(20),
    month       INT,
    quarter     INT,
    year        INT
);
```

## Creating the Fact Table

```sql
CREATE TABLE fact_sales (
    sale_id     INT PRIMARY KEY,
    customer_id INT REFERENCES dim_customer(customer_id),
    product_id  INT REFERENCES dim_product(product_id),
    date_id     INT REFERENCES dim_date(date_id),
    quantity    INT,
    revenue     DECIMAL(10, 2)
);
```

## Loading Sample Data

```sql
INSERT INTO dim_customer VALUES
    (501, 'Maria Chen', 'West', '2022-01-15'),
    (502, 'James Patel', 'East', '2023-06-02');

INSERT INTO dim_product VALUES
    (20, 'Wireless Mouse', 'Electronics', 'TechBrand'),
    (45, 'Notebook, Ruled', 'Office Supplies', 'PaperCo');

INSERT INTO fact_sales VALUES
    (1001, 501, 20, 3001, 2, 39.98),
    (1002, 502, 45, 3001, 1, 12.50);
```

## Querying Across Fact and Dimension

```sql
SELECT
    p.category,
    SUM(f.revenue) AS total_revenue
FROM fact_sales f
JOIN dim_product p ON f.product_id = p.product_id
GROUP BY p.category;
```

## Steps to Follow

1. Define the grain, stating exactly what one fact row represents.
2. Identify the numeric measures to be tracked.
3. Identify the descriptive context needed around those measures.
4. Create dimension tables first, since the fact table references them.
5. Create the fact table with foreign keys to each dimension.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Fact tables store measurable, numeric business events, along with foreign keys to related dimensions.
- The grain of a fact table defines exactly what one row represents, and every measure must match that grain.
- Dimension tables store descriptive context, such as customer or product details.
- Separating facts from dimensions avoids repeating descriptive data across every fact row.
- Business questions are typically answered by joining fact tables to dimension tables and aggregating the results.

With fact and dimension tables defined, the next module looks at how they are arranged together into a complete schema, most commonly the star schema.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
