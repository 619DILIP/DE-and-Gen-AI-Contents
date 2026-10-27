<br>

The focus of this section is `schema`, however it is impossible to implement schema in an RDBMS without the use of SQL. The way to implement a schema is to first create it, this step is dependent on the database vendor. Generally the syntax is:

```SQL
create schema <schema_name>;
```

After the schema has been created the data is divided in tables.

```SQL
create table <table_name> (
    <col_name> datatype constraint1 constraint2 ...,
    ...
);
```

A full schema is created using multiple create statements that define each table and those table relationships.
