# Implementation 

## Working with Variables and Data Types in Python:

### Variable Declaration and Assignment:

#### Integer Variable:

```python
age = 30
```

- In this example, a variable named age is declared and assigned an integer value of 30.

#### Float Variable:

```python
height = 1.75
```

- This line creates a variable height and assigns a floating-point value (decimal) of 1.75 to it.

#### String Variable:

```python
name = "John Doe"
```

- The variable name is initialized with a string value "John Doe", enclosed in double quotes.

#### Boolean Variable:

```python
is_valid = True
```

- Here, a boolean variable is_valid is assigned the value True, which represents a true condition.

### Data Type Inference:

#### Python infers data types automatically:

```python
num = 42  # Integer
pi = 3.14  # Float
message = "Hello"  # String
```
- Python automatically determines the data type of variables based on the value assigned. num is inferred as an integer, pi as a float, and message as a string.

### Type Conversion:

#### Implicit Type Conversion:

```python
num_int = 42
num_float = num_int + 0.5  # Implicitly converts integer to float
```

- Implicit type conversion occurs when different data types are combined in operations. Here, num_int is implicitly converted to a float when added to 0.5.

#### Explicit Type Conversion:

```python
num_str = "123"
num_int = int(num_str)  # Explicitly converts string to integer
```

- Explicit type conversion is done using built-in functions like int(), float(), str(), etc. Here, num_str is converted from a string to an integer using int().

### Variable Naming:

#### Following naming conventions:

```python
first_name = "Alice"  # snake_case for variable names
num_attempts = 5  # descriptive variable names
```

- Variable names should follow conventions like using lowercase letters and underscores for readability (snake_case). Descriptive names like first_name and num_attempts enhance code clarity.

### Checking Data Types:

#### Using the type() function:

```python
num = 42
print(type(num))  # Output: <class 'int'>
```
- The `type()` function is used to determine the data type of a variable. Here, it confirms that num is of type integer (int).

### Composite Data Types:

#### Lists:

```python
numbers = [1, 2, 3, 4, 5]
```

- Lists are used to store collections of items. Here, numbers is a list containing integers from 1 to 5.

#### Tuples:

```python
point = (10, 20)
```

- Tuples are similar to lists but are immutable (cannot be changed). point is a tuple containing coordinates (10, 20).

#### Dictionaries:

```python
person = {"name": "Alice", "age": 30}
```

- Dictionaries store key-value pairs. person is a dictionary with keys "name" and "age", mapping to values "Alice" and 30, respectively.

#### Sets:

```python
unique_numbers = {1, 2, 3, 4, 5}
```

- Sets are unordered collections of unique items. unique_numbers is a set containing unique integers from 1 to 5.
