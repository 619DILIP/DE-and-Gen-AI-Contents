<br>

```sql
-- Create a table with a UNIQUE constraint allowing NULL values
CREATE TABLE students (
    studentId INT UNIQUE,
    firstName VARCHAR(255),
    lastName VARCHAR(255)
);

-- Insert rows with unique non-null values and multiple NULL values
-- This is valid, as NULL values are not considered duplicates for the UNIQUE constraint
INSERT INTO students (studentId, firstName, lastName) VALUES
    (1, 'Jane', 'Smith'),
    (2, 'Suzanne', 'Brown'),
    (NULL, 'Abdul', 'Singh'),
    (NULL, 'Soria', 'Waler');

```

In the example above, we can see the use of the `UNIQUE` constraint, as well as columns that lack this constraint. Notice that we have two students who do not have a student ID, represented by Null values. 
This may represent that their student account profiles are pending some information, so we have not generated a student ID for them, or perhaps these students moved and no longer have an active student Id, although we still keep records of them in our database.

The first and last name columns may or may not contain duplicate values so it is possible to have matching values for both first and last name (two students named “John Doe” for instance).