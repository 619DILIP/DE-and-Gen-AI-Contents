<br>

The general syntax for creating a table in MySQL is:

``` sql
CREATE TABLE [IF NOT EXISTS] table_name(  
    column_definition1,  
    column_definition2,  
    ........,  
    table_constraints  
);
```
Example:

``` sql
CREATE TABLE movies(m_name VARCHAR(45) NOT NULL,m_genre VARCHAR(20) NOT NULL,m_director VARCHAR(30) NOT NULL,m_year INT NOT NULL,PRIMARY KEY(m_name));
```
Add values to the newly created table.

``` sql
INSERT INTO movies VALUE("Mr.Bean", "comedy", "Mr.ABC", 2019);
INSERT INTO movies VALUE("Fox", "horror", "Mr.XYZ", 2020);
```

### DROP vs TRUNCATE

The general syntax for dropping a table in MySQL is:


``` sql
DROP TABLE table_name;
```

We use `DROP` command to completely remove the table. Example:

``` sql
DROP TABLE movies;
```

The general syntax for truncating a table in MySQL is:


``` sql
TRUNCATE TABLE table_name;
```
The `TRUNCATE` command is used to delete the data inside a table, but not the table itself. Example:

``` sql
TRUNCATE TABLE movies;
```

### Modifying structure


To `ADD` a column:

``` sql
ALTER TABLE table_name
ADD column_name datatype;
```

We use `ALTER TABLE` command to modify a table. Example:

``` sql
ALTER TABLE movies
ADD ticket_price INT;
```

To `DROP` a column:

``` sql
ALTER TABLE table_name
DROP COLUMN column_name;
```
Example:

``` sql
ALTER TABLE movies
DROP COLUMN m_genre;
```

To `MODIFY` a column:

``` sql
ALTER TABLE table_name
MODIFY COLUMN column_name datatype;
```

Example:

``` sql
ALTER TABLE movies
MODIFY COLUMN ticket_price double;
```
