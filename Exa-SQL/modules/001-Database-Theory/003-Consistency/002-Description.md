
## Database Consistency

Database consistency is where all data points within the database system must align in order to be properly read and accepted. Information that does not meet the predefined values within the database will result in consistency errors with the dataset. Any transactions with the database involved in data written to the database must adhere to the database's established rules by developers. This is defined by specific constraints, triggers, variables, cascades, etc, that will all be described in the modules to follow.

While database consistency helps ensure the appropriate format for data written to the database, it does not account for what the data respresents. This means the information entered may match the appropriate format, but doesn't guarantee that the data corresponds with the actual information. 

These rules applied to our data is what keeps databases working smoothly by keeping inconsistent data out, achieving higher accuracy, increasing database space, and improving data retrieval.

## Database Inconsistency

Database consistency also applies to any changes of the data within the system. If one particular object in the database is updated, but also is present in another table in the database, it must be properly updated in all other tables it is present. If this fails, it results in database inconsistency.

Database inconsistency is when any portion of the information is updated in the table, but is not represented in all other tables utilizing that same information.