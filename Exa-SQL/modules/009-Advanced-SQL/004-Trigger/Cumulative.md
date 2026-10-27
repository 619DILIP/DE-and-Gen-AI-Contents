<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:
- Describe the use of triggers in a database.
- Create and delete a trigger.

</details>
<details><summary>Description</summary>
<br>

A trigger is a named SQL unit that is stored in the database and runs in response to an event that occurs in the database or when there is a modification to the database. You can specify the event, whether the trigger fires before or after the event, and whether the trigger runs for each event or for each row affected by the event.

For example, you can create a trigger that runs every time an `INSERT` statement affects the `EMPLOYEES` table.

</details>
<details><summary>Real World Application</summary>
<br>

Real-world applications include:

- Decisions that enforce business rules.
- Validating input data.
- Performing cascade operations when related records are changed.

</details>
<details><summary>Implementation</summary> 
<br>

Syntax to create a trigger:
```SQL
CREATE TRIGGER [trigger_name] 
    [BEFORE | AFTER]  
    {INSERT | UPDATE | DELETE}  
    ON [table_name]  
    [FOR EACH ROW]  
    [trigger_body] 
```

We can define six types of triggers for each table: 
- AFTER INSERT: activated after data is inserted into the table. 
- AFTER UPDATE: activated after data in the table is modified. 
- AFTER DELETE: activated after data is deleted from the table. 
- BEFORE INSERT: activated before data is inserted into the table. 
- BEFORE UPDATE: activated before data in the table is modified. 
- BEFORE DELETE: activated before data is deleted from the table. 

Example:
```
CREATE TRIGGER student_grade 
BEFORE INSERT 
ON Student 
FOR EACH ROW 
SET Student.total = Student.subj1 + Student.subj2 + Student.subj3, 
Student.perc = Student.total * 50 / 100;
```

Syntax to delete a trigger:
```SQL
DROP TRIGGER [IF EXISTS] trigger_name;
```
</details>
<details><summary>Summary</summary> 
<br>

- A trigger is a named SQL unit that is stored in the database and runs in response to an event that occurs in the database.
- You can specify the event, whether the trigger fires before or after the event, and whether the trigger runs for each event or for each row affected by the event.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
