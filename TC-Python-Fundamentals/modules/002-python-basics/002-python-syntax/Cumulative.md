<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:

* Describe the basic rules of Python syntax
* Describe standard conventions for writing Python code

</details>

<details><summary>Description</summary>
<br>

* Every programming language has specific syntax rules that must be followed for an application to run correctly. Python is no different.

* When working with and reading Python code, there are two important concepts to understand: __conventions__ and __syntax rules__.

* __Conventions__ are recommended practices that help developers write code that is consistent, readable, and easy for others to understand. Your code can still work even if you do not follow every convention.

* __Syntax rules__, on the other hand, are required. If you violate Python's syntax rules, your code will not run.

</details>

<details><summary>Real World Application</summary>
<br>

* Following Python's standard naming conventions is not required, but it provides significant benefits. When developers use the same conventions, it becomes much easier to read, understand, and maintain each other's code. In many cases, you can identify the purpose of a variable, class, or constant simply by how it is named.

* Syntax rules are different. If your code does not follow Python's syntax, the interpreter will raise an error and your program will not execute.

</details>

<details><summary>Implementation</summary>

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

</details>

<details><summary>Summary</summary>

# Summary

* Python conventions improve the readability and consistency of your code but are generally not required for it to run.
* Python syntax rules must be followed for your code to execute successfully.
* Following standard naming conventions makes your code easier for you and other developers to understand.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
