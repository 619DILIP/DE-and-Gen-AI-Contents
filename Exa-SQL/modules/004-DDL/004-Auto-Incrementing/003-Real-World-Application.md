<br>

Consider a table where we want to keep track of users. Users should not have the same identifier so as a new user is added to the database we would want to auto-increment their id. 

Table: Users

```sql
CREATE TABLE users (
 user_id SERIAL PRIMARY KEY,
 first_name VARCHAR(30),
 last_name VARCHAR(30),
 address VARCHAR(30),
 city VARCHAR(30),
 state VARCHAR(2),
 zip VARCHAR(5),
 social_number VARCHAR(11),
 username VARCHAR(30),
 password TEXT,
 email VARCHAR(50)
);
```



