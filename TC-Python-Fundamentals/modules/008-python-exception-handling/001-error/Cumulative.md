# Error
<details><summary>Learning Objectives</summary>
<br> 

* Understand the concept of errors in Python
* Learn about different types of errors in Python
* Identify and interpret error messages
* Develop strategies to handle and resolve errors
* Practice error-handling techniques

</details>
<details><summary>Description</summary>

# Introduction

As you progress in your programming journey, you will encounter various types of errors. In most programming languages, whenever an error halts program execution, an **`error message`** is displayed, providing crucial information about the error, including its location and type.

For instance, consider the following Python code:

```python
print("hi")
print "there"
```

When we execute this program, we would encounter the following error message:

```
File "/path/to/file.py", line 2
print "there"
     ^
SyntaxError: Missing parentheses in call to 'print'
```

This error message contains valuable information that can help us identify and resolve the issue. Let's break it down:

![Example](Images/Error-python.png)

1. **`File and Line Number (Location):`** The error message begins by indicating the file path and line number where the error occurred: **`File "/path/to/file.py", line 2`**. This information is crucial for locating the problematic code in your program.
2. **`Code Line with Error (Location):`** The next line displays the actual line of code where the error was detected: **`print "there"`**. This helps you quickly identify the specific statement causing the issue.
3. **`Error Indicator (Location):`** The caret symbol **`^`** points to the exact position in the code line where the error was encountered. In this case, it highlights the missing parentheses around the string argument in the **`print`** statement.
4. **`Error Type and Description:`** Finally, the error message provides the specific type of error (**`SyntaxError`**) and a brief description of the error: **`Missing parentheses in call to 'print'`**. This information helps you understand the nature of the problem and guides you toward resolving it.

Error messages are designed to assist developers in identifying and resolving issues within their code. By carefully examining the information provided in the error message, including the file path, line number, code line, error indicator, and error type/description, you can pinpoint the root cause of the problem and take appropriate steps to fix it.

It is essential to pay close attention to error messages and not ignore them, as they can save you significant time and effort in debugging your code. With practice, you will become proficient in interpreting error messages and leveraging the provided information to enhance your programming skills and write more robust and error-free code.

</details>
<details><summary>Real World Application</summary>
<br>

Handling errors is a crucial aspect of software development, as it ensures that applications are robust and can recover gracefully from unexpected situations. Error handling is essential in various real-world scenarios, such as:

1. **`User Input Validation:`** Handling errors when dealing with user input to prevent crashes or unexpected behavior.
2. **`File Operations:`** Catching and handling errors that may occur when working with files, such as file not found or permission issues.
3. **`Network Operations:`** Handling network-related errors, such as connection failures or timeouts, in network applications.
4. **`Database Operations:`** Dealing with errors that may occur during database interactions, such as invalid queries or connection issues.
5. **`API Integrations:`** Handling errors returned by third-party APIs to gracefully manage failures and provide appropriate responses.

</details>
<details><summary>Implementation</summary> 

## Common Types of Errors:

### Syntax Error:

A SyntaxError is a common issue that arises when the Python interpreter encounters code that does not adhere to the language's syntax rules. This error occurs during the parsing stage, where the interpreter analyzes your code to ensure it conforms to the language's grammar. Several factors can contribute to the occurrence of a SyntaxError, including:

* Unclosed strings
* Improper indentation
* Incorrect usage of the assignment operator (=)
* Misspelling of Python keywords
* Missing brackets, parentheses, or braces
* Attempting to use newer Python syntax on an older version of the language

When a SyntaxError occurs, Python generates a traceback, providing valuable information to help you pinpoint the issue's location. The traceback includes details such as the file name, line number, and a visual representation indicating where the invalid syntax was encountered, often accompanied by a helpful error message or question.

For instance, consider the following code snippet:

```python
employees = {"pam" 30,
             "jim": 28}
             
for name, age in employees.items():
    print(f"{name.capitalize()} is {age} years old.")
```

In this example, the syntax is invalid because the dictionary's first property lacks a colon (**`:`**) to separate the property **`"pam"`** and the value **`30`**. When executed, the following traceback is produced:

```
ERROR!
Traceback (most recent call last):
  File "<main.py>", line 1
    employees = {"pam" 30,
                    ^^^^^^^^
SyntaxError: invalid syntax. Perhaps you forgot a comma?
```

The traceback message has multiple carets (**`^`**) showing where the invalid syntax was encountered. While it sometimes might not pinpoint the exact location, it will usually hint at the issue's probable location.

To address this issue, carefully consider the following information in the traceback:

* File name
* Line number
* Location indicated by the caret (^)
* Error message, which can offer insights into the nature of the problem.
* The question added at the end of the error message provides valuable context.

To catch syntax errors before you execute the code, configure a linter within your code editor, such as Pylint or Flake8, to statically analyze the code.

In the code below, Pylance is used to highlight problematic areas with a red underline in VS Code:

![Example](Images/SyntaxError.png)

### Indentation Error:

The **`IndentationError`** in Python occurs when there is an issue with the indentation in your code. Common causes of this error include mixing tabs with spaces, incorrect spacing, incorrectly nested blocks, or whitespace at the beginning of a statement or file.

Consider the following example:

```python
if True:
print("Incorrectly indented")
```

This code triggers a Python traceback similar to:

```
ERROR!
Traceback (most recent call last):
  File "<main.py>", line 2
    print("Incorrectly indented")
    ^^^^^
IndentationError: expected an indented block after 'if' statement on line 1
```

The traceback message highlights the line where the indentation error was encountered and provides a descriptive error message, indicating that an indented block was expected after the 'if' statement on line 1.

To address and prevent this issue, use an editor or IDE configured with formatters like Black, which auto-formats your code as you write. The previously mentioned Pylance linter can also help you identify indentation errors:

![Example](Images/IndentationError.png)

The image above shows an error message indicating an issue with incorrect indentation. The error message at line 2 states "Incorrectly indented" and provides the expected indented block for the Python `print()` function definition.

The code snippet below the error message is not actual code but rather a documentation string or docstring explaining the `print()` function. This docstring shows the expected syntax, parameters, and a brief description of what the `print()` function does, which is printing values to a stream or sys.stdout by default.

![Example](Images/errorIndent.png)

So, the linter is pointing out improper indentation in the actual code being analyzed, and the included docstring serves as a reference for the correct formatting and usage of the `print()` function in Python.

### Name Error:

The **`NameError`** in Python is raised when an attempt is made to access an identifier (variable, function, or class) that has not been defined or is out of scope. Other potential causes of this error include referencing a variable before its assignment or misspelling an identifier.

Consider the following example:

```python
print(name)
```

In this case, the variable **`name`** is not defined, but it is being accessed, which results in Python throwing an exception:

```
ERROR!
Traceback (most recent call last):
  File "<main.py>", line 1, in <module>
NameError: name 'name' is not defined
```

The traceback message clearly indicates that the error occurred because the identifier `name` was not defined before being referenced.

To resolve a **`NameError`**, it is essential to ensure that the variable, function, or class name you intend to use has been adequately defined and is within the correct scope. Carefully review your code for any spelling errors or instances where a variable might be referenced before its assignment.

Additionally, setting up a linter in your editor will help you catch such problems early in the development process:

![Example](Images/NameError.png)

The image above shows an error message indicating an issue with a name error. The error message at line 1 states that 'name' is not defined and provides the expected name block for the Python `print()` function definition.

### Value Error:

The **`ValueError`** exception in Python indicates that a function has received an argument of the correct data type; however, the value itself is invalid or incompatible with the function's expectations. This error commonly occurs when attempting to convert a string or other data type to a numeric value, where the string representation does not conform to the expected format.

For example, consider the following code:

```python
num = int("forty-two")
```
function expects a string representation of an integer value. However, the provided string "forty-two" does not meet this requirement, leading Python to throw an exception:

 ERROR!
 Traceback (most recent call last):
 File "<main.py>", line 1, in <module>
 ValueError: invalid literal for int() with base 10: 'forty-two'

The traceback message clearly indicates that the string "forty-two" is an invalid literal for the **`int()`** function when using base 10 (decimal representation).

Another common cause of **`ValueError`** is passing an empty iterable to built-in functions like **`max()`** or **`min()`**, which expect non-empty iterables to operate on.

To resolve a **`ValueError`**, it is crucial to provide the correct data type and value as an argument to the respective function. Carefully review the function's documentation to ensure compliance with the expected input formats and value ranges.

In situations where user input is involved, it is recommended to use **`try-except`** blocks to gracefully handle potential input errors and prevent **`ValueError`** occurrences that could cause your program to crash. This approach allows you to catch the exception, provide appropriate feedback or error handling, and maintain a seamless user experience.

By adhering to best practices, validating user input, and leveraging exception handling mechanisms, you can effectively mitigate the occurrence of **`ValueError`** and enhance the robustness and reliability of your Python applications.

### Type Error:

The **`TypeError`** exception in Python is raised when an operation or function is performed on an object that is not supported or appropriate for its data type. This error occurs when the types of the operands involved in an operation or the arguments passed to a function are incompatible with the expected types.

For example, consider the following code:

 print("hello" / 3)

In this case, the attempt to divide a string ("hello") by an integer (3) is an unsupported operation, as division is not defined for strings. This code produces a **`TypeError`** exception with the following traceback:

 ERROR!
 Traceback (most recent call last):
 File "<main.py>", line 1, in <module>
 TypeError: unsupported operand type(s) for /: 'str' and 'int'

The traceback message clearly indicates that the operand types ('str' and 'int') are unsupported for the division operation (**`/`**).

A **`TypeError`** can also occur in situations such as:

* Attempting to iterate over a non-iterable object (e.g., a float or an integer)
* Providing incorrect argument types to built-in methods or functions (e.g., passing an integer to the **`len()`** function, which expects an iterable)
* Calling a function with fewer arguments than required
* Comparing or attempting to perform operations on different data types without appropriate type conversion

To avoid **`TypeError`** exceptions, it is essential to ensure the following:

1. Only iterate over iterable sequences (lists, tuples, strings, etc.).
2. Use arguments that match the expected types in built-in functions and methods.
3. Supply the correct number of arguments when calling a function, as specified by its definition.
4. Perform appropriate type conversions or comparisons when dealing with different data types.

By adhering to these practices and thoroughly understanding the expected data types for operations and functions, you can effectively mitigate the occurrence of **`TypeError`** exceptions and enhance the robustness and reliability of your Python code.

### ZeroDivision Error:

The **`ZeroDivisionError`** in Python is raised when an attempt is made to divide a number by zero, which is an undefined operation in mathematics. This error is a subclass of the **`ArithmeticError`** exception and is thrown to prevent the program from performing an illegal division by zero operation.

Consider the following example:

 result = 5 / 0
        
 print(result)

In this case, Python will raise a **`ZeroDivisionError`** with the following traceback:

 ERROR!
 Traceback (most recent call last):
 File "<main.py>", line 1, in <module>
 ZeroDivisionError: division by zero

The traceback message clearly indicates that the error occurred due to an attempt to divide by zero.

To avoid this error, it is crucial to ensure that the denominator is not zero before performing the division operation. One strategy to accomplish this is to check the value of the denominator explicitly:

 numerator = 5
 denominator = 0

 if denominator != 0:
 result = numerator/denominator

 else:
 print("Division by zero avoided.")

In this example, the program first checks if the denominator is not equal to zero before performing the division. If the denominator is not zero, the division is carried out, and the result is assigned to the **`result`** variable. Otherwise, a message is printed to indicate that the division by zero was avoided.

By implementing such checks and safeguards, you can prevent the occurrence of **`ZeroDivisionError`** and ensure that your program handles division operations safely and gracefully.

It is important to note that while division by zero is an illegal operation in mathematics, some programming languages or libraries may handle it differently, such as returning a special value (e.g., **`inf`** or **`NaN`**) or raising a different exception. Therefore, it is essential to consult the documentation of the specific language or library you are using to understand how division by zero is handled and what precautions should be taken.

### FileNotFound Error:

The **`FileNotFoundError`** exception in Python is raised when an attempt is made to perform file-related operations, such as reading, writing, or deleting a file that does not exist in the specified location. This error occurs when the program tries to access a file that cannot be found at the given file path.

Consider the following example:

 Traceback (most recent call last):
 File "/home/stanley/code_samples/main.py", line 1, in <module>
 with open('file_does_not_exist.txt', 'r') as file:
 FileNotFoundError: [Errno 2] No such file or directory: 'file_does_not_exist.txt'

In this case, Python is attempting to open a file named 'file_does_not_exist.txt' in read mode ('r'), but the file does not exist in the specified location, resulting in the **`FileNotFoundError`** being raised.

To resolve this issue, it is essential to ensure that the file exists at the specified location before attempting to perform any file operations. Double-checking the file path, file extension, and considering relative or absolute paths to the file can help prevent such errors.

However, in scenarios where the program receives incorrect file paths from users or external sources, it is advisable to implement exception handling using a **`try-except`** block to gracefully handle the **`FileNotFoundError`**. This approach prevents the program from crashing and allows for appropriate error handling or alternative actions.

 file_path = 'file_does_not_exist.txt'

 try:
 with open(file_path, 'r') as file:
 content = file.read()
                
 # Additional file processing code can go here
 except FileNotFoundError:
 print(f"The file '{file_path}' does not exist.")

 except Exception as e:
 print(f"An unexpected error occurred: {e}")

In this example, the program attempts to open the specified file and read its content. If the file does not exist, the **`FileNotFoundError`** is caught, and an appropriate message is printed. Additionally, a catch-all **`except`** block is included to handle any other unexpected exceptions that may occur during the file operations.

By implementing proper exception handling and providing clear error messages, you can create robust and user-friendly programs that gracefully handle situations where files are not found, ensuring a seamless user experience and preventing program crashes.

### Key Error:

A **`KeyError`** in Python is raised when an attempt is made to access a value in a dictionary using a key that does not exist within that dictionary. This error can occur if the specified key is missing, if there is a typographical error, or if the dictionary is empty.

Consider the following example:

 my_dict = {'name': 'John', 'age': 25}

 print(my_dict['location'])  # the 'location' key does not exist

In this case, the dictionary **`my_dict`** does not contain a key named 'location'. Attempting to access the value associated with this non-existent key results in a **`KeyError`** with the following traceback:

 ERROR!
 Traceback (most recent call last):
 File "<main.py>", line 2, in <module>
 KeyError: 'location'

The traceback message clearly indicates that the 'location' key is not found in the dictionary.

To avoid a **`KeyError`**, it is essential to verify the presence of the key in the dictionary and ensure that there are no typographical errors. Alternatively, the **`dict.get()`** method can be used, which allows you to provide a default value to be returned if the specified key is not found in the dictionary.

 my_dict = {'name': 'John', 'age': 25}

 print(my_dict.get('location', None))

In this example, the **`get()`** method is used to retrieve the value associated with the 'location' key. If the key is not found, **`None`** is returned as the default value.

For a more robust approach, you can handle the result of the **`get()`** method accordingly:

 my_dict = {'name': 'John', 'age': 25}

 location = my_dict.get('location')

 if location is not None:
 print("Location:", location)

 else:
 print("Location key not found in the dictionary.")

In this case, the program first retrieves the value associated with the 'location' key using **`get()`**. If the value is not **`None`** (i.e., the key exists in the dictionary), the location is printed. Otherwise, a message indicating that the key was not found is displayed.

By implementing such checks and utilizing the **`get()`** method, you can ensure that your program handles dictionary lookups gracefully and avoids unhandled exceptions.
method, you can effectively prevent `KeyError` occurrences and handle situations where a key is not present in a dictionary, ensuring that your code handles dictionary operations safely and gracefully.

### Attribute Error:

An **`AttributeError`** in Python is raised when an attempt is made to access or utilize an attribute (method or property) that an object or class does not possess. This error typically occurs due to a mismatch between the expected attributes of an object and the actual attributes available for that object's type.

Consider the following example:

```
my_list = [1, 2, 3]
        
print(my_list.lower())
```

In this case, the **`lower()`** method is being called on the **`my_list`** object, which is a list. However, the list type in Python does not have a **`lower()`** method defined, as it is typically used for string manipulation. Attempting to access this non-existent attribute results in an **`AttributeError`** with the following traceback:

```
ERROR!
Traceback (most recent call last):
  File "<main.py>", line 2, in <module>
AttributeError: 'list' object has no attribute 'lower'
```

The traceback message clearly indicates that the **`list`** object does not have the **`lower`** attribute.

To prevent **`AttributeError`**, it is essential to ensure that you are using attributes and methods that are actually available for the given object. This can be achieved by consulting the object's documentation or using tools like Mypy for static analysis.

Mypy, a static type checker for Python, can detect such issues early in the development process. For the above example, Mypy would indicate a problem as follows:

```
main.py:2: error: "list[int]" has no attribute "lower"  [attr-defined]
Found one error in 1 file (checked one source file)
```

By utilizing static analysis tools like Mypy, you can catch potential **`AttributeError`** issues before running your code, improving the overall quality and reliability of your Python applications.

Additionally, it is crucial to verify the correct spelling of attribute names and ensure that you are accessing attributes that are appropriate for the object's type. With careful attention to documentation and proper use of static analysis tools, you can effectively prevent **`AttributeError`** occurrences and ensure that your code interacts with objects and their attributes in a safe and predictable manner.

### Index Error:

The **`IndexError`** in Python occurs when an attempt is made to access an index in a sequence, such as a list, tuple, or string, that is outside the valid range of indices for that sequence. This error is typically encountered when trying to access an index that is either negative or greater than or equal to the length of the sequence.

Consider the following example:

```
numbers = [10, 20, 30]

numbers[4]
```

In this case, the **`numbers`** list has only three elements, with valid indices ranging from 0 to 2. Attempting to access index 4, which is out of range, results in the following exception:

```
ERROR!
Traceback (most recent call last):
  File "<main.py>", line 2, in <module>
IndexError: list index out of range
```

The traceback message clearly indicates that the index being accessed is out of range for the list.

To prevent **`IndexError`**, it is essential to ensure that the index being accessed falls within the valid range of indices for the sequence. This can be achieved by comparing the index with the sequence's length, which can be obtained using the **`len()`** function.

```
numbers = [10, 20, 30]

# Ensure the index is within the range of the list
index = 4
        
if index < len(numbers):
    print(numbers[index])
else:
    print("Index out of range")
```

In this example, the program first checks if the index is less than the length of the **`numbers`** list. If the condition is true, it proceeds to access and print the element at the specified index. Otherwise, it prints a message indicating that the index is out of range.

By implementing such checks and validations, you can effectively prevent **`IndexError`** occurrences and ensure that your code handles list or sequence indexing operations safely and gracefully.

It's worth noting that in addition to lists, **`IndexError`** can also occur when working with other sequence types, such as tuples and strings. Therefore, it's crucial to be mindful of index ranges when accessing elements in any sequence-like data structure in Python.

</details>
<details><summary>Summary</summary> 
<br>

* Errors in Python are instances where something goes wrong during program execution.
* Python provides various types of errors, such as syntax errors, runtime errors, and logical errors.
* Error messages help identify and resolve issues in the code.
* Error handling techniques, such as try-except blocks and raising exceptions, allow for graceful recovery from errors.
* Proper error handling is essential for building robust and reliable applications.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
