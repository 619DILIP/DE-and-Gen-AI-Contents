<br>

- `WHERE` clause is used to filter the data from the table based on user needs.
- `GROUP BY` clause is used in MySQL queries to organize records which have same attribute values.
- `ORDER BY` clause is used in MySQL queries to return the records in a sorted manner. By default, it returns in ascending order, which can also be specified as `ASC`. To return in descending order, We mention `DESC` after the expression along with `ORDER BY`.
- The difference between `ORDER BY` and `GROUP BY`

| ORDER BY | GROUP BY |
| ------------- | ------------- |
| It ensures presentation of columns  | It ensures presentation of rows  |
| It is always used after the GROUP BY clause in SELECT statement |  It is always used before the ORDER BY clause in SELECT statement  |
| It is not mandatory to use aggregate functions in the ORDER BY | It is mandatory to use aggregate functions in the GROUP BY  |
| The output is sorted based on the column's attribute values | The grouping of records is done based on the similarity among the row's attribute values |