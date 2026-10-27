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
