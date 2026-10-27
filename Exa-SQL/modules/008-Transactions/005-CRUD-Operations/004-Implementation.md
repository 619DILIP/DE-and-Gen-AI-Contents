<br>

- Basic Syntax for **C**reate Operations you've seen previously

```sql
CREATE TABLE TABLE_NAME (
    col_1 INT PRIMARY KEY, 
    col_2 VARCHAR(20), 
    col_N INT
);

INSERT INTO TABLE_NAME (column1, column2, columnN)
VALUES (value1, value2, valueN);
```

- Basic Syntax for **R**ead Operations you've seen previously

```sql
SELECT * FROM TABLE_NAME;

SELECT col_1, col_N
FROM TABLE_NAME
WHERE id = 1;
```

- Basic Syntax for **U**pdate Operations you've seen previously

```sql
UPDATE TABLE_NAME
SET column1 = value1, column2 = value2, columnN = valueN
WHERE [condition]
```

- Basic Syntax for **D**elete Operations you've seen previously

```sql
DELETE FROM TABLE_NAME
WHERE [condition];
```