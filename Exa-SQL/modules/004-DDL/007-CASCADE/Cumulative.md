<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:

- Define the `CASCADE` keyword
- Implement examples of `CASCADE`
- Differentiate between a `CASCADE` with `DELETE` and `UPDATE`

</details>
<details><summary>Description</summary>
<br>

In SQL, `CASCADE` is a keyword used to simultaneously delete or update data from both the child and parent tables and is used in conjunction with `ON DELETE` or `ON UPDATE`. Applying the `CASCADE` keyword to the command modifies the changes in both parent and child tables according to the execution of that query. `CASCADE` is appended to the reference command for the foreign key when creating a table.

## ON DELETE

Appending `ON DELETE CASCADE` to the foreign keys within our child table allows us the opportunity to delete the parent record and subsequently delete all relational information in any referenced table through one command. Otherwise, due to referential integrity, it would require multiple commands to delete all of the referenced records inside the child tables first before removing the parent record.

## ON UPDATE

Appending `ON UPDATE CASCADE` to the foreign key within our child table allows us to update information in a single command. By updating the parent table record, changes will apply to all subsequent child tables' information. This also helps reduce the number of commands and keeps our referential integrity intact.
</details>
<details><summary>Real World Application</summary>
<br>

Imagine students enrolled in courses at a college, but some students drop out mid-way through the semester, and the school is not required to keep the records of students who drop out. In this example, we would want to structure our tables such that the foreign keys have an `ON DELETE CASCADE` to maintain referential integrity when removing those students' records from the gradebooks of all courses they attended.

Continuing with the student examples, imagine the students in the database need their primary key IDs reset to account for the students that dropped out and make room for the freshmen. Through this, we need to update all the current records for each of these individuals to match accordingly in both the parent and child tables. When the foreign key is applied with `ON UPDATE CASCADE`, it will ensure that every record's primary key association in the child tables is updated accordingly.
</details>
<details><summary>Implementation</summary> 
<br>

Sticking with the college student theme, let's look at students in a college course and use `CASCADE` to handle deletions and updates.

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

- Finally, let's define a junction table to handle enrollment and use `CASCADE`
    - For the purposes of this example, we will assume that courses never get updated

```sql
CREATE TABLE enrollments(
    course_id INT,
    student_id INT,
    grade INT,
    completion_status BOOLEAN,
    PRIMARY KEY(course_id, student_id),
    FOREIGN KEY(course_id) REFERENCES courses(course_id) ON DELETE CASCADE,
    FOREIGN KEY(student_id) REFERENCES students(student_id) ON DELETE CASCADE ON UPDATE CASCADE
);
```

- The above command allows for the deletion of all referenced courses through a single command by removing the record from the courses table. Along with this, the command also accounts for any updates or deletions within the student table records.
</details>
<details><summary>Summary</summary> 
<br>

In SQL, `CASCADE` is a keyword used to simultaneously delete or update data from both the child and parent tables and is used in conjunction with `ON DELETE` or `ON UPDATE`. 
- `ON DELETE CASCADE` allows us, with one command, to delete records in a parent table and all subsequent records in the child tables. 
- `ON UPDATE CASCADE` allows us, with one command, to update records in a parent table and all subsequent records in the child tables.  
</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
