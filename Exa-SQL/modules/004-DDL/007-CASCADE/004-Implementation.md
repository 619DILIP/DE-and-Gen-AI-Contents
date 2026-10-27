<br>

Sticking with the students in college theme let's look at students in a college course and use `CASCADE` to handle deletions and updates.

- Define the table for students

```sql
CREATE TABLE students(
    student_id INT PRIMARY KEY,
    student_name VARCHAR(40),
    email VARCHAR(20) UNIQUE
);
```

- Define the table for courses

```sql
CREATE TABLE courses(
    course_id INT PRIMARY KEY,
    course_name VARCHAR(20),
    course_length_weeks INT,
    credits INT
);
```

- Finally, lets define a junction table to handle enrollment and uses `CASCADE`
    - for the purposes of this example we will assume that courses never get updated

```sql
CREATE TABLE enrollments(
    course_id INT,
    student_id INT,
    grade INT,
    completion_status boolean,
    PRIMARY KEY(course_id, student_id),
    FOREIGN KEY(course_id) REFERENCES courses(course_id) ON DELETE CASCADE
    FOREIGN KEY(student_id) REFERENCES students(student_id) ON DELETE CASCADE ON UPDATE CASCADE
);
```

- The above command allows for the deletion of all referenced courses through a single command by removing the record from the courses table. Along with this, the command also accounts for any updates or deletion within the students table records.