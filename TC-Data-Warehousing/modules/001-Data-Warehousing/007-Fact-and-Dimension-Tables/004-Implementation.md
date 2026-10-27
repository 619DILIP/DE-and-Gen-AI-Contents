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
