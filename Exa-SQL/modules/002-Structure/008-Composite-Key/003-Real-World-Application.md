<br>

Consider a scenario where there is a `student` table, `mentor` table, and another table named `mentor_mentee`. A student can have multiple mentors, and a mentor can have multiple students. In this type of relationship, the `mentor_mentee` table stores pairings between a student and their mentor. Records in the student table can be uniquely identified by `student id`, records in mentor table can be identified by `mentor id`, but the table `mentor_mentee` needs both `student id` and `mentor id` to uniquely identify a record. Both `student id` and `mentor id` are grouped as a primary key.
