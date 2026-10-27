<br>

- Basic SQL `JOIN` Clause syntax, using `INNER JOIN` to show basic syntax.

```sql
SELECT 
TABLE_NAME1.column1, TABLE_NAME1.columnN, TABLE_NAME2.column1, TABLE_NAME2.columnN
FROM TABLE_NAME1
INNER JOIN TABLE_NAME2
ON TABLE_NAME1.matching_column = TABLE_NAME2.matching_column;
```
