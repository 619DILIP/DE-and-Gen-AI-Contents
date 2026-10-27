<details><summary>Learning Objectives</summary>
<br>

- Understand the concept of variables and their role in Python programming.
- Learn about different data types available in Python and their characteristics.
- Explore variable naming conventions and best practices.

</details>

<details><summary>Description</summary>
<br>

Variables in Python are used to store and manipulate data. A variable is essentially a named storage location in memory where you can store values.

Python is dynamically typed, meaning you don't need to explicitly declare the data type of a variable. Instead, Python infers the data type based on the value assigned to the variable.

## Introductory Concepts about Variables and Data Types:

### Variables: 

> Named storage locations are used to hold data during program execution.

### Data Types:

> Different types of data can be stored in variables, such as integers, floats, strings, booleans, lists, tuples, dictionaries, and more.

### Dynamic Typing:

> Python automatically determines the data type of a variable based on the value assigned to it.

## Key Characteristics of Variables and Data Types:

### Fundamental Data Types:

> Basic data types in Python include integers, floats, strings, booleans, and None.

### Composite Data Types:

> Composite or collection data types include lists, tuples, sets, and dictionaries, used for storing collections of data.

### Type Conversion:

> Python allows implicit and explicit type conversion between different data types using built-in functions and constructors.

### Variable Naming:

> Variables in Python should follow naming conventions, such as using descriptive names, avoiding reserved words, and using lowercase with underscores for readability (snake_case).

Understanding how to use variables and work with different data types is essential for writing effective and efficient Python code.

</details>

<details><summary>Real World Application</summary>

## Variables and Data Types in Python are commonly used for:

### Data Storage and Manipulation:

> Storing and processing data of various types, including numbers, text, collections, and more.

### Program Logic and Control:

> Using variables to store intermediate results, control flow, and decision-making in algorithms and scripts.

### User Input and Output:

> Handling user input, formatting output, and displaying information in user interfaces or command-line applications.

### Data Analysis and Processing:

> Analyzing data, performing calculations, and applying algorithms to structured and unstructured data sets.

Variables and data types are fundamental concepts in programming and are used extensively in software development, data science, automation, and other domains.

</details>

<details><summary>Implementation</summary> 

## Working with Variables and Data Types in Python:

### Variable Declaration and Assignment:

#### Integer Variable:

```python
age = 30
```

- In this example, a variable named `age` is declared and assigned an integer value of 30.

#### Float Variable:

```python
height = 1.75
```

- This line creates a variable `height` and assigns a floating-point value (decimal) of 1.75 to it.

#### String Variable:

```python
name = "John Doe"
```

- The variable `name` is initialized with a string value "John Doe", enclosed in double quotes.

#### Boolean Variable:

```python
is_valid = True
```

- Here, a boolean variable `is_valid` is assigned the value `True`, which represents a true condition.

### Data Type Inference:

#### Python infers data types automatically:

```python
num = 42  # Integer
pi = 3.14  # Float
message = "Hello"  # String
```
- Python automatically determines the data type of variables based on the value assigned. `num` is inferred as an integer, `pi` as a float, and `message` as a string.

### Type Conversion:

#### Implicit Type Conversion:

```python
num_int = 42
num_float = num_int + 0.5  # Implicitly converts integer to float
```

- Implicit type conversion occurs when different data types are combined in operations. Here, `num_int` is implicitly converted to a float when added to 0.5.

#### Explicit Type Conversion:

```python
num_str = "123"
num_int = int(num_str)  # Explicitly converts string to integer
```

- Explicit type conversion is done using built-in functions like `int()`, `float()`, `str()`, etc. Here, `num_str` is converted from a string to an integer using `int()`.

### Variable Naming:

#### Following naming conventions:

```python
first_name = "Alice"  # snake_case for variable names
num_attempts = 5  # descriptive variable names
```

- Variable names should follow conventions like using lowercase letters and underscores for readability (snake_case). Descriptive names like `first_name` and `num_attempts` enhance code clarity.

### Checking Data Types:

#### Using the `type()` function:

```python
num = 42
print(type(num))  # Output: <class 'int'>
```
- The `type()` function is used to determine the data type of a variable. Here, it confirms that `num` is of type integer (`int`).

### Composite Data Types:

#### Lists:

```python
numbers = [1, 2, 3, 4, 5]
```

- Lists are used to store collections of items. Here, `numbers` is a list containing integers from 1 to 5.

#### Tuples:

```python
point = (10, 20)
```

- Tuples are similar to lists but are immutable (cannot be changed). `point` is a tuple containing coordinates (10, 20).

#### Dictionaries:

```python
person = {"name": "Alice", "age": 30}
```

- Dictionaries store key-value pairs. `person` is a dictionary with keys "name" and "age", mapping to values "Alice" and 30, respectively.

#### Sets:

```python
unique_numbers = {1, 2, 3, 4, 5}
```

- Sets are unordered collections of unique items. `unique_numbers` is a set containing unique integers from 1 to 5.

</details>

<details><summary>Summary</summary> 
<br>

- Variables in Python are named storage locations used to store and manipulate data during program execution.

- Python supports various data types, including integers, floats, strings, booleans, None, lists, tuples, sets, dictionaries, and more.

- Data types in Python can be inferred automatically or explicitly specified using constructors and conversion functions.

- Following naming conventions and best practices for variable naming enhances code readability and maintainability.

- Understanding variables and data types is fundamental for programming logic, data manipulation, and algorithm implementation in Python.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
