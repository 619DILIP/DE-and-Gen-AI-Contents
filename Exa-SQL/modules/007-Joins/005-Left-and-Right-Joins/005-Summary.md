<br>

* `LEFT JOIN` allows us to get all the entries from Table1 and those records from Table2 that meet the join criteria.
  * If there is no match in Table2 for a record in Table1, the result will still include the record from Table1, but with `NULL` values for columns from Table2.
* `RIGHT JOIN` allows us to get all the entries from Table2 and those records from Table1 that meet the join criteria. 
  * If there is no match in Table1 for a record in Table2, the result will still include the record from Table2, but with `NULL` values for columns from Table1.

**Syntax LEFT JOIN**: 

SELECT column_name(s)  
FROM table1  
LEFT JOIN table2  
ON table1.column_name = table2.column_name;

**Syntax RIGHT JOIN**: 

SELECT column_name(s)  
FROM table1  
RIGHT JOIN table2  
ON table1.column_name = table2.column_name;
