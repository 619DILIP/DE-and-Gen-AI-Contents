<br>

The DCL sublanguage provides a means of defining access control to a database and its objects. Privileges can be granted or revoked on users.

## Privileges

A database can have numerous privileges which can be permitted to users. Below is a summary of more common privileges.

| Privilege | Description                        |
| --------- | ---------------------------------- |
| `SELECT`    | allows `SELECT` statements on tables |
| `INSERT`    | allows `INSERT` statements on tables |
| `DELETE`    | allows `DELETE` statements on tables |
| `UPDATE`    | allows `UPDATE` statements on tables |
| `INDEX`    | allows creating indexes on tables  |
| `CREATE`    | allows `CREATE` table statements     |
| `ALTER`     | allows `ALTER` table statements      |
| `DROP`     | allows `DROP` table statements       |
| `ALL`       | allow all permissions except `GRANT` |
| `GRANT`     | allows `GRANT` statements            |

## GRANT

The `GRANT` command is used to add permissions to a user. To `GRANT` permissions, the user executing the statement must have the `GRANT` permission.

```sql
GRANT PRIVILEGES ON object TO user;
```

To `GRANT` a simple privilege like `SELECT` on a table named 'posts' to a user named 'john.user'.

```sql
GRANT SELECT ON posts TO 'john.user';
```

To `GRANT` all of the CRUD abilities on a table named 'posts' to a user named 'community.manager'.

```sql
GRANT SELECT,  INSERT, UPDATE, DELETE ON posts TO 'community.manager';
```

## Revoke

The `REVOKE` command is used to remove permissions from a user.

```sql
REVOKE PRIVILEGES ON object FROM user;
```

To revoke the `SELECT` privilege on the 'posts' table from 'john.user'

```sql
REVOKE SELECT ON posts FROM 'john.user';
```

To remove the CRUD privileges on 'posts' from 'community.manager'.

```sql
revoke SELECT, INSERT, UPDATE, DELETE ON posts FROM 'community.manager';
```
