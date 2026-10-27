
## Syntax to create a sequence

In PostgreSQL:
```SQL
CREATE SEQUENCE sequence_name
    [ INCREMENT BY increment ]
    [ START WITH start ]
    [ MAXVALUE max_value | NO MAXVALUE ]
    [ MINVALUE min_value | NO MINVALUE ]
    [ CYCLE | NO CYCLE ];

```

- sequence_name: Name of the sequence.
- START WITH: Starting value from where the sequence starts. 
- INCREMENT BY: Value by which sequence will increment itself. Increment_value can be positive or negative.
- MAXVALUE: Maximum value of the sequence.
- MINVALUE: Minimum value of the sequence.
- CYCLE: When sequence reaches its set_limit it starts from beginning.
- NOCYCLE: An exception will be thrown if the sequence exceeds its max_value.


Example 1:
```SQL
CREATE SEQUENCE example_1
AS INT
START WITH 10
INCREMENT BY 10; 
```

Example 2:
```SQL
CREATE SEQUENCE example_2
start with 100
increment by -1
minvalue 1
maxvalue 100
cycle;
```