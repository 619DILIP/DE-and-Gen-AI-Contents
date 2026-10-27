
### Examples

Counting the amount of records in a table:
```SQL
SELECT COUNT(*) FROM EMP;    
```

Counting the values of a particular column:
```SQL
SELECT COUNT(EMP_NAME) FROM EMP;   
```

Finding the sum of all values from a specific field:
```SQL
SELECT SUM(duration) AS "Total duration" FROM EMP;
```

Calculating the average of the values from specified columnL
```SQL
SELECT AVG(salary) FROM EMP;
```

Finding the minimum salary:
```SQL
SELECT MIN(salary) FROM EMP;    
```

Finding the maximum salary:
```SQL
SELECT MAX(salary) FROM EMP; 
```