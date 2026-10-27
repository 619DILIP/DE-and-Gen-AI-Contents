<br>

| `DROP`  | `CREATE` | `TRUNCATE` |
| ------------- | ------------- | ------ |
| It removes a table form the database | It creates a new table with no information, along with views, procedures, schemas, indexes and databases | It is executed using table lock, where whole table is locked while removing the records |
| It maintains the log, so it is slower than `TRUNCATE` | It maintains the log | Least amount of logging needed so it is faster in performace |
| It cannot be rolled back | It cannot be rolled back | It cannot be rolled back |
