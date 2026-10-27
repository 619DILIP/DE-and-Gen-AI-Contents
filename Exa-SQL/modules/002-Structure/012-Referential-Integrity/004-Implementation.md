<br>

step 1: Create a table named Student.

``` sql
 CREATE TABLE Student(
    student_id INT PRIMARY KEY,
    first_name VARCHAR(20),
    last_name VARCHAR(20),
    Major VARCHAR(20)
    );

```
Step 2: create a table named InternationalStudent.

``` sql
CREATE TABLE InternationalStudent(
    country_id INT PRIMARY KEY,
    name VARCHAR(20),
    student_id INT,
    FOREIGN KEY(student_id) REFERENCES Student(student_id)
    ON DELETE CASCADE
);
```
Step 3: Insert values into Student table and InternationalStudent table.
``` sql
INSERT INTO Student VALUES(1,"Taylor", "Swift","English Literature");
INSERT INTO Student VALUES(2,"Stephen", "Hawking","Physics");
INSERT INTO InternationalStudent VALUES(1,"USA",1);
INSERT INTO InternationalStudent VALUES(2,"UK",2);
```
``` sql
SELECT * FROM InternationalStudent;
```
Result:
| country_id | name  | student_id |
|------------|-------|------------|
|     1      | USA   |          1 |
|     2      | UK    |          2 |

Step 4: delete a record from Student table
``` sql
DELETE FROM Student WHERE Major="English Literature";
```
Now the record in child table InternationalStudent with student_id as 1 is deleted.

``` sql
SELECT * FROM InternationalStudent;
```
Result:
| country_id | name  | student_id |
|------------|-------|------------|
|     2      | UK    |          2 |




