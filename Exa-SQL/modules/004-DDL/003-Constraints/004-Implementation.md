<br>

Adding constraints to a column can be done when the table is being created or afterward if the requirements should change. Specific disscussion on the command associated with creating or altering tables is out of the scope of this document, but will discussed in the appropriate section.

```SQL
-- adding constraints during creation
create table <table_name> (
    <col_name> datatype constraint1 constraint2,
    constraint <constraint_name> <constraint_type>(constraint_option, ...)
)
```

```SQL
-- adding constraints after creation
alter table <table_name> add constraint <constraint_name> <constraint_type>(constraint_option, ...)
```

<hr/>

## Exercises (Optional)

Discuss how to model a table for a rideshare application. The table will be called "scheduled_pickups". As the name suggests, the table should manage riders who have scheduled rides immediately and in the future.
