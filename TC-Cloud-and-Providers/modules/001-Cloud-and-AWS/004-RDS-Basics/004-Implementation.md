## Creating a Database Instance

1. Open the RDS service in the AWS Management Console.
2. Select a database engine, such as PostgreSQL or MySQL.
3. Choose an instance size appropriate to the expected workload.
4. Set a master username and a strong password.
5. Configure network access so only trusted sources can reach the database.
6. Enable automated backups and set a retention period.

## Finding the Connection Endpoint

Once the instance is available, the console displays an endpoint address used for connections.

```text
mydb.abc123xyz.us-east-1.rds.amazonaws.com
```

## Connecting from Python

```python
import os
import psycopg2

connection = psycopg2.connect(
    host=os.environ.get("RDS_HOST"),
    port=5432,
    database="salesdb",
    user=os.environ.get("RDS_USER"),
    password=os.environ.get("RDS_PASSWORD")
)

cursor = connection.cursor()
cursor.execute("SELECT COUNT(*) FROM orders;")
print(cursor.fetchone())

cursor.close()
connection.close()
```

Credentials are read from environment variables rather than written into the code.

## Creating a Table

```python
cursor = connection.cursor()
cursor.execute("""
    CREATE TABLE IF NOT EXISTS orders (
        order_id    INT PRIMARY KEY,
        customer_id INT,
        order_date  DATE,
        amount      DECIMAL(10, 2)
    )
""")
connection.commit()
```

## Steps to Follow

1. Create the RDS instance with an appropriate engine and size.
2. Restrict network access to specific trusted sources.
3. Store the connection credentials outside of application code.
4. Test the connection before writing pipeline logic against it.
5. Confirm automated backups are enabled and retained appropriately.