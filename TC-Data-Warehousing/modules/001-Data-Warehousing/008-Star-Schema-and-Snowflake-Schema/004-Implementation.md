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
