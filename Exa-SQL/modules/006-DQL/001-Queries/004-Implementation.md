<br>

Syntax to create database:

``` sql
CREATE DATABASE WORK;
```

Syntax to select/use database:

``` sql
USE WORK;
```

Syntax to create TABLE:

``` sql
CREATE TABLE EMP
(id INT, NAME VARCHAR(25), AGE INT, PRIMARY KEY(id));
```

Syntax to alter TABLE:

``` sql
ALTER TABLE EMP
ADD SALARY DOUBLE;
```

Syntax to insert values:

``` sql
INSERT INTO EMP VALUES(111, "Ryan", 24, 5000);
```

Syntax to update record:

``` sql
UPDATE EMP SET AGE = 23 WHERE id = 111;
```

Syntax to delete record:

``` sql
DELETE FROM EMP WHERE id = 111;
```

Syntax to select record:

``` sql
SELECT * FROM EMP;
```

Syntax to truncate table:

``` sql
TRUNCATE TABLE EMP;
```

Syntax to drop table:

``` sql
DROP TABLE EMP;
```
