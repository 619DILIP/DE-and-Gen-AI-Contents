<br>

- Basic Syntax Implementation for `UPDATE`

```sql
UPDATE TABLE_NAME
SET column1 = value1, column2 = value2, columnN = valueN
WHERE [condition];
```

- Example of `UPDATE` for Single Record in employee with id = 12 Address
    - NOTE: Double check the ID whenever you use these commands to make sure you're updating the appropriate record

```sql
UPDATE employees
SET add_street = 'Philly Lane', add_number = '20211', add_zip = 19101
WHERE employee_id = 12;
```

- Example of `UPDATE` for Multiple Records in Employee to transfer department_name from "QC" to "Tech"

```sql
UPDATE employees
SET department_name = 'Tech'
WHERE department_name = 'QC';
```