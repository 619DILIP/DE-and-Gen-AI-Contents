<br>

Syntax to create a trigger:
```SQL
create trigger [trigger_name] 
    [before | after]  
    {insert | update | delete}  
    on [table_name]  
    [for each row]  
    [trigger_body] 
```

We can define 6 types of triggers for each table: 
- AFTER INSERT activated after data is inserted into the table. 

- AFTER UPDATE: activated after data in the table is modified. 

- AFTER DELETE: activated after data is deleted/removed from the table. 

- BEFORE INSERT: activated before data is inserted into the table. 

- BEFORE UPDATE: activated before data in the table is modified. 

- BEFORE DELETE: activated before data is deleted/removed from the table. 

Example:
```
create trigger student_grade 
before INSERT 
on 
Student 
for each row 
set Student.total = Student.subj1 + Student.subj2 + Student.subj3, 
Student.perc = Student.total * 50 / 100;
```

Syntax to delete a trigger
```SQL
DROP TRIGGER [IF EXISTS] trigger_name
```