# Introduction 

What do you do when something bad happens in your program? Let’s say you try to open a file, but you type in the wrong path, or you ask the user for information, and they type in some garbage. You don’t want your program to crash, so you implement exception handling.

Exception handling in Python is a process of resolving errors that occur in a program. This involves catching exceptions, understanding what caused them, and responding accordingly. Exceptions are errors that occur at runtime when the program is being executed. They are usually caused by invalid user input or code that is invalid in Python. Exception handling allows the program to continue to execute even if an error occurs.

Syntax:

    try:
        # code that may cause an exception
    
    except ExceptionType as e:
        # code to handle the exception
    
    else:
        # code to execute if no exceptions were raised
    
    finally:
        # code that will always be executed, regardless of exceptions

   
### Exception Handling Mechanism

Exception handling in python is managed by the following 3 keywords:

* try
* catch or except
* finally
* Throw or raise

 
### Try Statement:

The try statement is used to handle exceptions that may occur within a block of code. It consists of the keyword 'try', followed by a colon (:), and a code block (suite) where potential exceptions might be raised. If no exceptions are raised during the execution of the try suite, the interpreter skips the associated exception handlers.

However, if an exception occurs within the try suite, the program control is transferred to the corresponding except handler that matches the type of exception raised. This process is known as catching the exception.
 
Syntax:

    try:
        statement(s)


### Catch/Except Statement:

The catch statement is responsible for handling specific types of exceptions that may be raised within the try block. Each catch block is designed to catch a particular type of exception, ranging from a specific exception to a general category of exceptions.
 
Here are the rules for catch blocks:

* A catch block is defined using the keyword 'catch'.
* The catch block specifies the type of exception it handles within parentheses.
* The code for handling the exception is written between curly braces {}.
* Multiple catch blocks can be associated with a single try block.
* Catch blocks should be ordered from the most specific exception type to the most general.
* A catch block can only be used after a try block.

Syntax:

    try:
        statement(s)

    except:
        statement(s)


### Finally Statement:

The finally statement introduces a block of code that will be executed regardless of whether an exception was raised or not in the try block. This block is typically used for cleanup operations that must be performed in all circumstances.

The finally block is optional, but it ensures that certain code is executed, even if an exception occurs or a return statement is encountered within the try block.

Syntax:

    try:
        statement(s)

    finally:
        statement(s)
  

### Raise Statement:

The raise statement is used to explicitly raise an exception. It can be used with or without arguments. When used without arguments, it re-raises the current exception. When used with arguments, it creates a new exception instance and raises it.

Syntax:

    raise [Exception [, args [, traceback]]]

In this syntax, the argument is optional, and at the time of execution, the exception argument value is always none.

 
### Try, Except, Else:

The try/except statement can also have an else clause. The else block is executed only if no exceptions are raised within the try block. This can be useful when you want to perform additional operations after successfully executing the try block without encountering any exceptions.

The else block is typically used when you want to execute a second piece of code that can also raise an exception, as any code following a try/except will be executed if no errors were raised.

It's important to note that the finally block, if present, will always be executed, regardless of whether an exception was raised or not.

We will spend a few moments looking at a couple examples:

    my_dict = {"a":1, "b":2, "c":3}

    try:
        value = my_dict["a"]

    except KeyError:
        print("A KeyError occurred!")

    else:
        print("No error occurred!")

Here we have a dictionary with 3 elements and in the try/except we access a key that exists. This works, so the KeyError is not raised. Because there is no error, the else executes and “No error occurred!” is printed to the screen. Now let’s add in the finally statement:

    my_dict = {"a":1, "b":2, "c":3}

    try:
        value = my_dict["a"]

    except KeyError:
        print("A KeyError occurred!")

    else:
        print("No error occurred!")

    finally:
        print("The finally statement ran!")

If you run this example, it will execute the else and finally statements. Most of the time, you won’t see the else statement used as any code that follows a try/except will be executed if no errors were raised. The only good usage of the else statement that I’ve seen mentioned is where you want to execute a second piece of code that can also raise an error. Of course, if an error is raised in the else, then it won’t get caught.

 