<br>

- The Syntax to use `WHERE` clause is:

``` sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

Example:

``` sql
SELECT title
FROM movies
WHERE ticket_price=200;
```

- The Syntax to use `ORDER BY` clause is:

``` sql
SELECT expressions    
FROM tables    
[WHERE conditions]    
ORDER BY expression [ ASC | DESC ];    
```

Example:

``` sql
SELECT marks
FROM STUDENTS
WHERE marks>60
ORDER BY marks DESC;
```

- The Syntax to use `GROUP BY` clause is:

``` sql
SELECT column_name, function(column_name)  
FROM table_name   
WHERE condition   
GROUP BY column_name;  
```

Example 1:

``` sql
SELECT Dept, Salary
FROM Employee
WHERE Salary > 15000
GROUP BY employee.salary, employee.dept
ORDER BY Dept DESC;
```
Example 2:

``` sql
SELECT Dept, AVG(Salary) as AvgSalary
FROM Employee
WHERE Salary > 15000
GROUP BY employee.dept
ORDER BY Dept DESC;
```
#### Let's break down the differences:

Column Selection:

- **Example 1:** Selects individual Dept and Salary values.
- **Example 2:** Selects Dept and the average Salary for each department.

GROUP BY clause:
        
- **Example 1:** Groups by both salary and department, which doesn't change the result set.
- **Example 2:** Groups only by department, allowing for aggregation of salaries within each department.

Aggregation:

- **Example 1:** No aggregation is performed.
- **Example 2:** Uses AVG() to calculate the average salary for each department.

#### When to use each approach:

**Example 1:**

- Use when you want to see individual salary records for each employee in departments where at least one employee earns more than $15,000.
- It's essentially equivalent to removing the GROUP BY clause entirely, as it doesn't change the result set.
- This query might be useful for getting a detailed view of high-earning employees across departments.

**Example 2:**

- Use when you want to analyze salary data at the department level.
- It provides a summary view, showing the average salary for each department (considering only salaries above $15,000).
- This is useful for comparing compensation across departments or identifying departments with higher average salaries.

#### The key difference is the level of detail and the type of analysis you're performing:

- The **Example 1** query gives you a granular view of individual salaries.
- The **Example 2** query provides an aggregated view, summarizing salary data by department.