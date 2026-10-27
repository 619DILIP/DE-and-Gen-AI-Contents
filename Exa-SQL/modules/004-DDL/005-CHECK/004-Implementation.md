<br>

An example table for the syntax is as follows. Please note that certain column names and attributes in this example would need to be modified depending on what you are trying to accomplish in your table. 

```sql
CREATE TABLE products (
    productID INT PRIMARY KEY,
    productPrice DECIMAL CHECK (productPrice > 0)
);
```

This particular example is checking that the `NumericColumn` contains values greater than 0. 

