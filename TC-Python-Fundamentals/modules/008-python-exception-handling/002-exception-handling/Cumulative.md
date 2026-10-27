<details><summary>Learning Objectives</summary>
<br>

1. Understand the concept of exceptions in Python programming.
2. Learn about the different types of exceptions and their meanings.
3. Explore how to use try-except blocks to handle exceptions.
4. Discover advanced exception handling techniques like try-except-else and try-except-finally.
5. Apply exception handling in real-world scenarios to write robust and reliable code.

</details>
<details><summary>Description</summary>
<br>

What do you do when something bad happens in your program? Let's say you try to open a file, but you type in the wrong path, or you ask the user for information, and they type in some garbage. You don't want your program to crash, so you implement exception handling.

Exception handling in Python is a process of resolving errors that occur in a program. This involves catching exceptions, understanding what caused them, and responding accordingly. Exceptions are errors that occur at runtime when the program is being executed. They are usually caused by invalid user input or invalid code in Python. Exception handling allows the program to continue to execute even if an error occurs.

Syntax:

 try:
 # code that may cause an exception
    
 except ExceptionType as e:
 # code to handle the exception
    
 else:
 # code to execute if no exceptions were raised
    
 finally:
 # code that will always be executed, regardless of exceptions

   
### Exception Handling Mechanism

Exception handling in Python is managed by the following three keywords:

* try
* except
* finally
* raise

 
### Try Statement:

The try statement is used to handle exceptions that may occur within a block of code. It consists of the keyword 'try', followed by a colon (:), and a code block (suite) where potential exceptions might be raised. If no exceptions are raised during the execution of the try suite, the interpreter skips the associated exception handlers.

However, if an exception occurs within the try suite, the program control is transferred to the corresponding except handler that matches the type of exception raised. This process is known as catching the exception.
 
Syntax:

 try:
 statement(s)


### Except Statement:

The except statement is responsible for handling specific types of exceptions that may be raised within the try block. Each except block is designed to catch a particular type of exception, ranging from a specific exception to a general category of exceptions.
 
Here are the rules for except blocks:

* An except block is defined using the keyword 'except'.
* The except block specifies the type of exception it handles within parentheses.
* The code for handling the exception is written between curly braces {}.
* Multiple except blocks can be associated with a single try block.
* Except blocks should be ordered from the most specific exception type to the most general.
* An except block can only be used after a try block.

Syntax:

 try:
 statement(s)

 except:
 statement(s)


### Finally Statement:

The finally statement introduces a block of code that will be executed regardless of whether an exception was raised or not in the try block. This block is typically used for cleanup operations that must be performed in all circumstances.

The finally block is optional, but it ensures that certain code is executed, even if an exception occurs or a return statement is encountered within the try block.

Syntax:

 try:
 statement(s)

 finally:
 statement(s)
  

### Raise Statement:

The raise statement is used to raise an exception explicitly. It can be used with or without arguments. When used without arguments, it re-raises the current exception. When used with arguments, it creates a new exception instance and raises it.

Syntax:

 raise [Exception [, args [, traceback]]]

In this syntax, the argument is optional, and at the time of execution, the exception argument value is always None.

 
### Try, Except, Else:

The try/except statement can also have an else clause. The else block is executed only if no exceptions are raised within the try block. This can be useful when you want to perform additional operations after successfully executing the try block without encountering any exceptions.

The else block is typically used when you want to execute a second piece of code that can also raise an exception, as any code following a try/except will be executed if no errors were raised.

It's important to note that the finally block, if present, will always be executed, regardless of whether an exception was raised or not.

We will spend a few moments looking at a couple examples:

 my_dict = {"a" :1, "b":2, "c":3}

 try:
 value = my_dict["a"]

 except KeyError:
 print("A KeyError occurred!")

 else:
 print("No error occurred!")

Here we have a dictionary with 3 elements, and in the try/except we access a key that exists. This works, so the KeyError is not raised. Because there is no error, the else executes, and "No error occurred!" is printed to the screen. Now let's add the finally statement:

 my_dict = {"a":1, "b":2, "c":3}

 try:
 value = my_dict["a"]

 except KeyError:
 print("A KeyError occurred!")

 else:
 print("No error occurred!")

 finally:
 print("The finally statement ran!")

If you run this example, it will execute the else and finally statements. Most of the time, you won't see the else statement used as any code that follows a try/except will be executed if no errors were raised. The only good usage of the else statement that I've seen mentioned is where you want to execute a second piece of code that can also raise an error. Of course, if an error is raised in the else, then it won't get caught.

</details>
<details><summary>Real World Application</summary>
<br>

Exception handling is a crucial aspect of software development, as it helps to ensure that applications can gracefully handle unexpected situations and continue running without crashing. Some real-world applications of exception handling include:

1. **`User Input Validation:`** Handling exceptions when dealing with user input to prevent crashes or unexpected behavior.
2. **`File Operations:`** Catching and handling exceptions that may occur when working with files, such as file not found or permission issues.
3. **`Network Operations:`** Handling network-related exceptions, such as connection failures or timeouts, in network applications.
4. **`Database Operations:`** Dealing with exceptions that may occur during database interactions, such as invalid queries or connection issues.
5. **`API Integrations:`** Handling exceptions returned by third-party APIs to gracefully handle failures and provide appropriate responses.

</details>
<details><summary>Implementation</summary> 

## Common Types of Exception:

### ArithmeticError: 
ArithmeticError serves as the base class for all arithmetic-related exceptions, and it is raised when an arithmetic operation fails or encounters an error. 

Example:

 try:
 result = 10 / 0  # Division by zero raises a ZeroDivisionError (subclass of ArithmeticError)

 except ArithmeticError as e:
 print(f"An arithmetic error occurred: {e}")

In this example, dividing 10 by 0 causes a **`ZeroDivisionError`**, which is a subclass of **`ArithmeticError`**. The except block catches the **`ArithmeticError`** and prints an appropriate message.


### ImportError: 
ImportError is raised when an attempt is made to import a module that is not found or cannot be imported due to various reasons, such as a typo in the module name or the module not being present in the system's module search path. 

Example:

 try:
 import non_existent_module

 except ImportError as e:
 print(f"An import error occurred: {e}")

In this example, an attempt is made to import a module named **`non_existent_module`**, which does not exist. As a result, an **`ImportError`** is raised, and the **`except`** block catches it and prints an appropriate message.


### IndexError: 
IndexError is raised when an attempt is made to access an index in a sequence (e.g., list, string, tuple) that is out of range or invalid. 

Example:

 my_list = [1, 2, 3]

 try:
 print(my_list[3])  # Accessing an index out of range

 except IndexError as e:
 print(f"An index error occurred: {e}")

In this example, an attempt is made to access the fourth element of a list with only three elements, resulting in an **`IndexError`**. The **`except`** block catches the **`IndexError`** and prints an appropriate message.


### KeyError: 
KeyError is raised when an attempt is made to access a non-existent key in a dictionary. 

Example:

 my_dict = {"a":1, "b":2, "c":3}

 try:
 value = my_dict["a"]

 except KeyError:
 print("A KeyError occurred!")

 else:
 print("No error occurred!")

 finally:
 print("The finally statement ran!")

In this example, we have a dictionary with three elements, and in the **`try/except`** we access a key that exists. This works, so the **`KeyError`** is not raised. Because there is no error, the **`else`** and **`finally`** execute, and "No error occurred!" and "The finally statement ran!" are printed to the screen. 


### NameError: 
NameError is raised when an attempt is made to access or use a name (variable, function, or other identifier) that has not been defined or assigned a value in the current scope (local or global namespace). 

Example:

 try:
 print(non_existent_variable)  # Accessing an undefined variable

 except NameError as e:
 print(f"A name error occurred: {e}")

In this example, an attempt is made to print the value of a variable named **`non_existent_variable`**, which has not been defined or assigned a value. As a result, a **`NameError`** is raised, and the **`except`** block catches it and prints an appropriate message.


### ValueError: 
ValueError is raised when a function or operation receives an argument of the correct type but an inappropriate or invalid value. 

Example:

 try:
int_value = int("abc")  # Attempting to convert a non-numeric string to an integer

except ValueError as e:
print(f"A value error occurred: {e}")

In this example, an attempt is made to convert the string **`abc`** (which is not a valid integer representation) to an integer using the **`int()`** function. As a result, a **`ValueError`** is raised, and the `except` block catches it and prints an appropriate message.

### EOFError:
EOFError (End of File Error) is raised when the **`input()`** function reaches an end-of-file condition without reading any data. This typically occurs when the user enters the end-of-file character (e.g., Ctrl+D on Unix or Ctrl+Z on Windows) instead of providing input.

Example:

try:
user_input = input("Enter some text: ")

except EOFError as e:
print(f"An EOF error occurred: {e}")

else:
print(f"You entered: {user_input}")

In this example, if the user enters the end-of-file character instead of providing input, an **`EOFError`** is raised. The `except` block catches the **`EOFError`** and prints an appropriate message. If no exception occurs, the `else` block is executed, and the user's input is printed.

### ZeroDivisionError:
ZeroDivisionError is a specific type of **`ArithmeticError`** that is raised when an attempt is made to divide a number by zero, which is an illegal operation in most cases.

Example:

try:
result = 10 / 0  # This will raise an ArithmeticError (ZeroDivisionError)

except ArithmeticError as e:
print(f"An arithmetic error occurred: {e}")

finally:
print("This block is always executed.")

In this example,

* The **`try`** block contains the code **`result = 10 / 0`**, which attempts to divide 10 by 0. This operation is illegal in mathematics and raises an **`ArithmeticError`**, specifically a **`ZeroDivisionError`** (a subclass of **`ArithmeticError`**).
* The **`except ArithmeticError as e`** block is executed when an **`ArithmeticError`** or any of its subclasses (like **`ZeroDivisionError`**) is raised within the **`try`** block. The error object is assigned to the variable **`e`**, and the **`print statement`** displays the error message using an f-string.
* The **`finally`** block is always executed, regardless of whether an exception was raised or not within the **`try`** block. In this case, it prints the string "This block is always executed."

### IOError:
IOError (Input/Output Error) is raised when an input/output operation fails, such as reading from or writing to a file or interacting with other input/output streams.

Example:

try:
with open("non_existent_file.txt", "r") as file:
contents = file.read()

except IOError as e:
print(f"An I/O error occurred: {e}")

In this example, an attempt is made to open a file named **`non_existent_file.txt`** for reading, but the file does not exist. As a result, an **`IOError`** is raised, and the `except` block catches it and prints an appropriate message.

### SyntaxError:
SyntaxError is raised when there is a syntax error or an invalid construct in the Python code, making it impossible for the interpreter to parse and execute the code.

Example:

try:
eval("print(hello)")  # Invalid syntax: missing quotes around 'hello'

except SyntaxError as e:
print(f"A syntax error occurred: {e}")

In this example, the **`eval()`** function attempts to evaluate the string **`print(hello)`**, which contains a syntax error (missing quotes around **`hello`**). As a result, a **`SyntaxError`** is raised, and the `except` block catches it and prints an appropriate message.

### IndentationError:
IndentationError is raised when the indentation of the Python code is incorrect or inconsistent, which violates the syntax rules of the language. Example:

try:
def my_function():
print("This line is indented correctly.")
print("This line is not indented correctly.")  # Incorrect indentation

except IndentationError as e:
print(f"An indentation error occurred: {e}")

In this example, the function **`my_function()`** is defined with correct indentation, but the subsequent **`print()`** statement is not indented correctly. As a result, an **`IndentationError`** is raised, and the `except` block catches it and prints an appropriate message.

</details>
<details><summary>Summary</summary>
<br>

* Exceptions in Python are objects that represent errors or exceptional conditions.
* Exception handling allows you to write robust and fault-tolerant code by catching and handling exceptions.
* The **`try-except`** statement is used to catch and handle exceptions in Python.
* Multiple exceptions can be caught using multiple **`except`** blocks or a bare **`except`** clause.
* The **`finally`** clause is executed regardless of whether an exception occurred or not.
* Proper exception handling is essential for building reliable and maintainable applications.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
