<br>

It's important to refer to the documentation of the specific database system you are using, as the syntax and supported data types for DEFAULT can vary between database management systems
```sql
CREATE TABLE UserOnline (
    ID INT PRIMARY KEY,
    UserName VARCHAR(25),
    Online BOOLEAN DEFAULT false
);
```

```sql
-- Inserting a user with online status not specified (defaults to false)
INSERT INTO UserOnline (ID, UserName) VALUES (1, 'LemonadeStandBoss');
```

```sql
-- Inserting a user with online status explicitly set to true
INSERT INTO UserOnline (ID, UserName, Online) VALUES (2, 'CodeLikeABoss', true);
```

In this example, the first user record inserted `(“LemonadeStandBoss”)` would have a value of `‘false’` for the column `‘Online’`, since no value was provided. Note that some SQL dialects may use the keyword `DEFAULT` as well within the insert statement.