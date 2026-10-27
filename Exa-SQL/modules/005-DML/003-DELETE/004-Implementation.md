<br>

- Basic Syntax for `DELETE` command

```sql
DELETE FROM TABLE_NAME
WHERE [condition];
```

- Example to `DELETE` Student, student_id = 'student1@uni.edu' from an enrollment table for course_id = 101

```sql
DELETE FROM enrollment
WHERE student_id = 'student1@uni.edu' AND course_id = 101;
```

- Example of `DELETE` all the above student's grades from a student_assessments table

```sql
DELETE FROM student_assessments
WHERE student_id = 'student1@uni.edu';
```