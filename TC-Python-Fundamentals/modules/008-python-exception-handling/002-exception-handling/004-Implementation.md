# Implementation

## Common Types of Exception:

### ArithmeticError: 
ArithmeticError serves as the base class for all arithmetic-related exceptions, and it is raised when an arithmetic operation fails or encounters an error. 

Example:

    try:
        result = 10 / 0  # Division by zero raises a ZeroDivisionError (subclass of ArithmeticError)

    except ArithmeticError as e:
        print(f"An arithmetic error occurred: {e}")

In this example, dividing 10 by 0 causes a **`ZeroDivisionError`**, which is a subclass of **`ArithmeticError`**. The except block catches the **`ArithmeticError`** and prints an appropriate message.


### ImportError: 
ImportError is raised when an attempt is made to import a module that is not found or cannot be imported due to various reasons, such as a typo in the module name or the module not being present in the system's module search path. 

Example:

    try:
        import non_existent_module

    except ImportError as e:
        print(f"An import error occurred: {e}")

In this example, an attempt is made to import a module named **`non_existent_module`**, which does not exist. As a result, an **`ImportError`** is raised, and the **`except`** block catches it and prints an appropriate message.


### IndexError: 
IndexError is raised when an attempt is made to access an index in a sequence (e.g., list, string, tuple) that is out of range or invalid. 

Example:

    my_list = [1, 2, 3]

    try:
        print(my_list[3])  # Accessing an index out of range

    except IndexError as e:
        print(f"An index error occurred: {e}")

In this example, an attempt is made to access the fourth element of a list with only three elements, resulting in an **`IndexError`**. The **`except`** block catches the **`IndexError`** and prints an appropriate message.


### KeyError: 
KeyError is raised when an attempt is made to access a non-existent key in a dictionary. 

Example:

    my_dict = {"a":1, "b":2, "c":3}

    try:
        value = my_dict["a"]

    except KeyError:
        print("A KeyError occurred!")

    else:
        print("No error occurred!")

    finally:
        print("The finally statement ran!")

In this example,  we have a dictionary with 3 elements and in the **`try/except`** we access a key that exists. This works, so the **`KeyError`** is not raised. Because there is no error, the **`else`** and **`finally`** executes and “No error occurred!” and “The finally statement ran!” are printed to the screen. 


### NameError: 
NameError is raised when an attempt is made to access or use a name (variable, function, or other identifier) that has not been defined or assigned a value in the current scope (local or global namespace). 

Example:

    try:
        print(non_existent_variable)  # Accessing an undefined variable

    except NameError as e:
        print(f"A name error occurred: {e}")

In this example, an attempt is made to print the value of a variable named **`non_existent_variable`**, which has not been defined or assigned a value. As a result, a **`NameError`** is raised, and the **`except`** block catches it and prints an appropriate message.


### ValueError: 
ValueError is raised when a function or operation receives an argument of the correct type but an inappropriate or invalid value. 

Example:

    try:
        int_value = int("abc")  # Attempting to convert a non-numeric string to an integer

    except ValueError as e:
        print(f"A value error occurred: {e}")

In this example, an attempt is made to convert the string **`abc`** (which is not a valid integer representation) to an integer using the **`int()`** function. As a result, a **`ValueError`** is raised, and the except block catches it and prints an appropriate message.


### EOFError: 
EOFError (End of File Error) is raised when the **`input()`** function reaches an end-of-file condition without reading any data. This typically occurs when the user enters the end-of-file character (e.g., Ctrl+D on Unix or Ctrl+Z on Windows) instead of providing input. 

Example:

    try:
        user_input = input("Enter some text: ")

    except EOFError as e:
        print(f"An EOF error occurred: {e}")

    else:
        print(f"You entered: {user_input}")

In this example, if the user enters the end-of-file character instead of providing input, an **`EOFError`** is raised. The **`except`** block catches the **`EOFError`** and prints an appropriate message. If no exception occurs, the **`else block`** is executed, and the user's input is printed.


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
IOError (Input/Output Error) is raised when an input/output operation fails, such as reading from or writing to a file, or interacting with other input/output streams. 

Example:

    try:
        with open("non_existent_file.txt", "r") as file:
            contents = file.read()

    except IOError as e:
        print(f"An I/O error occurred: {e}")

In this example, an attempt is made to open a file named **`non_existent_file.txt`** for reading, but the file does not exist. As a result, an **`IOError`** is raised, and the **`except`** block catches it and prints an appropriate message.


### SyntaxError: 
SyntaxError is raised when there is a syntax error or an invalid construct in the Python code, making it impossible for the interpreter to parse and execute the code. 

Example:

    try:
        eval("print(hello)")  # Invalid syntax: missing quotes around 'hello'

    except SyntaxError as e:
        print(f"A syntax error occurred: {e}")

In this example, the **`eval()`** function attempts to evaluate the string **`print(hello)`**, which contains a syntax error (missing quotes around **`hello`**). As a result, a **`SyntaxError`** is raised, and the **`except`** block catches it and prints an appropriate message.


### IndentationError: 
IndentationError is raised when the indentation of the Python code is incorrect or inconsistent, which violates the syntax rules of the language. Example:

    try:
        def my_function():
            print("This line is indented correctly.")
        print("This line is not indented correctly.")  # Incorrect indentation

    except IndentationError as e:
        print(f"An indentation error occurred: {e}")

In this example, the function **`my_function()`** is defined with correct indentation, but the subsequent **`print()`** statement is not indented correctly. As a result, an **`IndentationError`** is raised, and the **`except`** block catches it and prints an appropriate message.

