## sqlite3 Module

To interact with SQLite3, you will need to import the `sqlite3` module in your code

```python
import sqlite3
```

Once you have access to the module, you can create a connection with your pre-existing SQLite3 database, or you can create one.
```python
# connects to a db if it exists, creates one if needed
# Use the name ":memory:" if you want the db to exist in memory only
sqlite_connection_in_memory_db = sqlite3.connect(":memory:")

sqlite_connection_persistent_db = sqlite3.connect("db_file")
```

Once you are connected to your database, you need a cursor object to query the database
```python
cursor = sqlite_connection.cursor()
```

That's it: you are ready to start querying your database. To do so, you pass your SQL query into the execute method:
```python
cursor.execute("select sqlite_version()")
```

Then you use a fetch method to return one or more records (stored in a tuple per record) returned by the query inside a list object
```python
result_all = cursor.fetchall()  # returns all the records
result_some = cursor.fetchmany(3)  # returns the first three records
result_one = cursor.fetchone()  # returns the next record in the list
```
If your query is a transaction, you will want to either commit the change to persist it or roll back to undo the work if a mistake is made.
```python
# persist your changes
sqlite_connection.commit()

# reverts to the previous commit
sqlite_connection.rollback()
```
When your operations with the cursor are complete, it is good practice to close the cursor and create a new cursor for any new actions. This helps to save system resources and keep your queries organized.
```python
# close when you finish operations with the cursor
cursor.close()

# open a new cursor to perform new operations
new_cursor = sqlite_connection.cursor()
```
Finally, when you are done working with the database, it is good practice to close your connection explicitly.
```python
sqlite_connection.close()
```