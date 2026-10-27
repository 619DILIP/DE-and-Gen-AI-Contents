<br>

A function in SQL serves a similar purpose to functions in dedicated programming and scripting languages. They perform some set of defined operations on given data and return a result. Functions in SQL are similar to procedures except functions return a value.

When creating a function, we give a definition of what our function has to do. We will have to call that function to perform the defined task as and when required. When a program calls a function, program control is switched to the respective function.

- Characteristics of a function include:
    - Functions are separate blocks that are mainly used for calculations or bundling common operations into a single call.
    - Functions with DML commands can be called from other blocks, but functions without DML commands are typically called using a SELECT query.
    - Arguments (input values) can be passed into functions when called by defining function parameters during function creation.
      - These parameters should be included in the calling statements.
    - A function uses the RETURN command to return the value or raise an exception. 
      - A return command is mandatory to create SQL functions, as it will always return the value, in calling statements it always accompanies with assignment operator to populate the variables.

Many SQL dialects and RDBMS' provide built-in functions for convenience, however, the creation of custom functions may be helpful to support a developer's specific database operations.
