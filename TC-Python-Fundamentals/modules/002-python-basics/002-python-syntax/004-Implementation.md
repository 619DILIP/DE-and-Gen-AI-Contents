## General Naming Conventions

Python developers commonly use three naming conventions: __SCREAMING\_SNAKE\_CASE__, __snake\_case__, and __PascalCase__. These are community conventions rather than language requirements, but following them makes your code easier to read and consistent with most Python projects.

Python identifiers may contain letters, numbers (after the first character), and underscores (`_`).

* __SCREAMING\_SNAKE\_CASE__
  * By convention, starts with an uppercase letter
  * Uses uppercase letters throughout
  * Individual words are separated with underscores
  * Example: `SCREAMING_SNAKE_CASE`

* __snake\_case__
  * By convention, starts with a lowercase letter
  * Individual words are separated with underscores
  * Example: `snake_case`

* __PascalCase__
  * By convention, starts with an uppercase letter
  * Each word begins with an uppercase letter and no underscores are used
  * Example: `PascalCase`

These naming conventions are commonly used for different kinds of objects in Python:

* __SCREAMING\_SNAKE\_CASE__ is typically used for values that should not change (for example, `PI`). Python does not enforce constants, but this naming convention signals that the value should be treated as one.
* __PascalCase__ is used for classes.
* __snake\_case__ is used for variables, functions, and most other names.

```python
name = "Bill Teddington"
other_name = "Sally Sussington"
```

The code above runs without errors. However, if the second line is indented, the code will no longer work:

```python
name = "Bill Teddington"
    other_name = "Sally Sussington"
```

Notice that the second line is indented even though no code block has been started. This results in an `IndentationError`. As you work through the modules, pay close attention to the formatting and syntax used in the examples.