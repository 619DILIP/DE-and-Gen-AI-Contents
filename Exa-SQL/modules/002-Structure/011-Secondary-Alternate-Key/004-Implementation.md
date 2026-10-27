<br>

The following table has a secondary key.

``` sql
CREATE TABLE Product (
    ProductID INT PRIMARY KEY,
    Barcode VARCHAR(20) UNIQUE,
    Name VARCHAR(100),
    Description TEXT,
    Price DECIMAL(10, 2)
);

```

In this example:

- ProductID is the primary key of the table.
- Barcode is a candidate key since the column is marked as UNIQUE, ensuring each value in that column is unique.
