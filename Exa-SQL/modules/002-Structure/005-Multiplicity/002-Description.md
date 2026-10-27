<br>

### Multiplicity vs Cardinality
Although these two terms are often used interchangeably, technically they are different. Generally, you can think of __multiplicity__ as the _possible range_ of associations between one entity and another. __Cardinality__ represents a _specific number_ of associations. For example, let's say we have an application to manage apartment buildings and we want to model two entities, a Person and a Pet. We want to have a constraint of each person having at most 2 pets. In ER Diagrams, the multiplicity could be seen as 0..2 or a range of 0 to 2 associations between Person and Pet. The cardinalities defined are 0 and 2. If there is no upper limit then we can use an asterisk (\*) rather than a number. For example, the multiplicity for the relationship between a social media influencer and their followers could be 0...*. 


We often look at multiplicity in simpler terms by just referring to a type of relationship entities can have with one another. 
- These relationships are:
    - **one to one relationship**
        - Definition: In a one-to-one relationship, each record in one table is associated with only one record in another table, and vice versa.
        - Example: A person might have only one passport, and each passport belongs to only one person.
        - Implementation: A one-to-one relationship can be implemented by adding a unique foreign key in one of the tables that references the primary key of the other table. Alternatively, both tables can share the same primary key.
    - **one to many relationship**
        - This is described from the perspective of the "one" side.
        - Definition: In a one-to-many relationship, a single record in the "one" table can be associated with multiple records in the "many" table.
        - Example: A single author can have multiple books. Here, "author" is the "one" side, and "books" are the "many" side.
        - Implementation: The "many" table (books) includes a foreign key that references the primary key in the "one" table (author).
    - **many to one relationship**
        - This is described from the perspective of the "many" side.
        - Definition: In a many-to-one relationship, multiple records in the "many" table can be associated with a single record in the "one" table.
        - Example: Many employees can belong to a single department. Here, "employees" are the "many" side, and "department" is the "one" side.
        - Implementation: The "many" table (employees) includes a foreign key that references the primary key in the "one" table (department).
    - **many to many relationship**
        - Definition: In a many-to-many relationship, multiple records in one table can be associated with multiple records in another table.
        - Example: A student can enroll in multiple courses, and each course can have multiple students enrolled in it.
        - Implementation: This type of relationship requires a junction table (also called a bridge or join table) that holds foreign keys referencing the primary keys of the two tables involved. For example, a student_courses table might store references to both student_id and course_id to track which students are in which courses.

**NOTE**: the difference between a one-to-many relationship and a many-to-one is strictly perspective. They are actually the same.