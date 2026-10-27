<br>

- Referential integrity  is used to build and maintain logical relationships between tables to avoid logical corruption of data.

- Referential integrity is made up of the combination of a primary key and a foreign key.

- Normally the table with a Primary key is considered as a parent table and the table with a foreign key is considered a child table.

- Updating and Deletion in primary key table and Insertion and Updating in the foreign key table could
violate the referential integrity.

- To avoid violating Referential Integrity, ON DELETE CASCADE, set the foreign key to NULL, or set foreign key to default are implemented.
