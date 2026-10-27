<br>

- `SELF JOIN` is a SQL statement which is used to intersect or join a table in the database to itself. We use it when we need to compare data within the same table. 
- This type of joining of data with other data in the same table when a condition is matched is also known as something called a Unary relationship.


![self](images/Self-join.jpg)

**Syntax**:   
SELECT column_name(s)  
FROM table1 T1, table1 T2  
WHERE condition;  