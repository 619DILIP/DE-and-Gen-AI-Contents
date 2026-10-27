<br>

- Syntax to `DROP` a table from database

``` sql
DROP TABLE table_name;
```

Example:

``` sql
DROP TABLE Movies;
```

- Syntax to `CREATE` a table 

``` sql
CREATE TABLE table_name{
    table_id INT PRIMARY KEY IDENTITY(1,1),
    table_value VARCHAR (50) NOT NULL,
    table_value INT,
    foreign_key INT
    FOREIGN KEY (foreign_id) REFERENCES foreign_table_name (foreign_id)
}
```

Example:

``` sql
CREATE TABLE courses (
    course_id INT PRIMARY KEY IDENTITY (1, 1),
    course_name VARCHAR (50) NOT NULL,
    max_capacity VARCHAR (50) NOT NULL,
    professor_id INT
    FOREIGN KEY (professor_id) REFERENCES professors (professor_id)
);
```

- Syntax to `TRUNCATE` a table from database

``` sql
TRUNCATE TABLE table_name;
```

Example:

``` sql
TRUNCATE TABLE student;
```
