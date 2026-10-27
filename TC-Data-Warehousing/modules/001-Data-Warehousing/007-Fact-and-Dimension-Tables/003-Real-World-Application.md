## Answering a Business Question

Consider the question "what was total revenue by product category last month." Answering this requires joining `Fact_Sales` to `Dim_Product` on `product_id`, filtering the fact table's date range, and summing the `revenue` measure grouped by the `category` column from the dimension table.

This pattern, joining a fact table to one or more dimension tables to add context before aggregating, is the single most common type of query run against a data warehouse. It is the direct reason fact and dimension tables are structured the way they are.
