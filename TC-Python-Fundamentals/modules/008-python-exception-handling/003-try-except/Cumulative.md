<details><summary>Learning Objectives</summary>
<br>

1. Understand the purpose and use of exception handling in Python.
2. Learn how to catch and handle different types of exceptions using the **`try`** and **`except`** statements.
3. Explore the use of multiple **`except`** blocks to handle different exceptions.
4. Understand the concept of the **`else`** and **`finally`** clauses in exception handling.

</details>
<details><summary>Description</summary>

# Introduction

In the realm of programming, writing code that can gracefully handle errors and exceptions is a fundamental aspect of developing robust and reliable software. Specifically, it is crucial to ensure that errors or exceptions do not cause critical failures that result in the abrupt termination of your program. This is where the **`try-except`** statement comes into play, particularly in Python.

The **`try-except`** statement is a powerful code block that allows your program to take alternative actions in case an error or exception occurs. It serves as a vital tool for handling exceptions, which are unexpected events that disrupt the normal flow of instructions during program execution. When an exception occurs, it can potentially cause the program to terminate abruptly, leading to undesirable consequences such as data loss or system instability.

Python's **`try-except`** block provides a controlled mechanism for handling exceptions, ensuring that your program can continue executing even in the face of unexpected errors. This robustness is achieved by enclosing the code that might raise an exception within a **`try`** block, followed by one or more **`except`** blocks that specify how to handle different types of exceptions.

Syntax:

```
try:
    # Code block 1 (There can be errors in this block)
    
except ExceptionName:
    # Code block 2 (Do this to handle exception)
    # executed if the try block throws an error
```

*try block:*
 * The **`try`** block is used to encapsulate the code that might raise an exception.
 * If no exception occurs during the execution of the code inside the **`try`** block, the **`except`** block(s) are skipped, and the program continues executing the next statement after the **`try`** statement.

*except block:*
 * The **`except`** block is used to catch and handle specific exceptions that might be raised by the code inside the **`try`** block.
 * After the keyword **`except`**, you specify the type of exception you want to catch, represented by **`ExceptionName`**.
 * If an exception of the specified type (**`ExceptionName`**) is raised inside the **`try`** block, the code inside the corresponding **`except`** block is executed.
 * You can have multiple **`except`** blocks to catch and handle different types of exceptions.
 * If no exception is raised, or if the exception raised is not the one specified in the **`except`** block, the **`except`** block is skipped, and the program continues executing the next statement after the **`try-except`** block.

### What Are the Differences Between Try-Catch and Try-Except?

Python and Java both have constructs for handling exceptions, but there are some notable differences between the two. While the fundamental concept of enclosing potentially error-prone code within a **`try`** block and handling exceptions in separate blocks remains the same, the syntax and additional features vary.

The syntax of the **`try-except`** block in Python is as follows:

```
try:
    # some code here that might raise an exception
except ExceptionType:
    # handle the exception here
```

In Java, the syntax for the **`try-catch`** block is as follows:

```
try {
    // some code here that might throw an exception
} catch (ExceptionType e) {
    // handle the exception here
}
```

In Python, the exception handling construct is known as **`try-except`**, whereas in Java, it's called **`try-catch`**. The primary difference lies in the availability of an additional **`else`** code block in Python, which is not present in Java's exception handling mechanism.

Python's Exception Handling:

* **`try:`** This block contains the code that might raise an exception.
* **`except:`** This block specifies the code to be executed when a specific exception occurs within the **`try`** block.
* **`else:`** This optional block contains code that will be executed if no exceptions are raised in the **`try`** block.
* **`finally:`** This optional block contains code that will be executed regardless of whether an exception occurred or not, typically used for cleanup tasks.

Java's Exception Handling:

* **`try:`** This block contains the code that might raise an exception.
* **`catch:`** This block specifies the code to be executed when a specific exception occurs within the **`try`** block.
* **`finally:`** This optional block contains code that will be executed regardless of whether an exception occurred or not, typically used for cleanup tasks.

The key distinction is the presence of the **`else`** block in Python's exception handling construct. In Python, if no exceptions are raised within the **`try`** block, the code within the **`else`** block will be executed. This feature is not available in Java's exception handling mechanism.

Java does not have a direct equivalent to Python's **`else`** block. If you need to execute code when no exceptions occur in Java, you typically place that code after the **`try-catch`** block or within the **`finally`** block, although the latter is generally reserved for cleanup tasks.

Both Python and Java have the **`finally`** block, which is executed regardless of whether an exception was raised or not. This block is commonly used for resource cleanup tasks, such as closing files or network connections.

It's important to note that while the **`else`** and **`finally`** blocks are optional in Python, only the **`finally`** block is optional in Java's exception handling construct.

### When to use try/except?

The **`try/except`** statement is used when you have a code block that may sometimes execute correctly and sometimes encounter errors, depending on conditions that you cannot foresee at the time of writing the code.

One common scenario where **`try/except`** is useful is when your code fetches data from a website. In such cases, your code may run into issues like a lack of network connection or the external website being temporarily unresponsive. If your program can still perform useful operations in these situations, you can handle the exception and allow the rest of your code to execute.

Another example involves extracting data from nested structures, such as dictionaries obtained from a website. When attempting to access specific elements, some keys or values may be missing. If you anticipate that a particular key might not be present, you could use an if-else check to handle the situation.

```
if some_key in d:
    # The key is present; extract the data
    extract_data(d)
else:
    skip_this_one(d)
```

However, if you need to extract multiple pieces of data, it can become tedious to check for each potential missing key or value. In such cases, you can wrap the data extraction code within a **`try/except`** block.

```
try:
    extract_data(d)
except:
    skip_this_one(d)
```

It is generally considered poor practice to catch all exceptions in this broad manner. Instead, Python provides a way to specify the types of exceptions you want to catch (for example, catching only **`KeyError`** exceptions, which occur when a key is missing from a dictionary).

```
try:
    extract_data(d)
except KeyError:
    skip_this_one(d)
```

By using the **`try/except`** statement, you can gracefully handle exceptions and ensure that your program continues to run even when encountering unexpected issues or missing data. This approach allows you to write more robust code that can adapt to varying conditions and prevent abrupt program termination due to errors.

</details>
<details><summary>Real World Application</summary>
<br>

Exception handling is crucial in scenarios where the input to a program is unpredictable or when dealing with external resources such as files or network connections. For example:

* In a web scraping script, handling exceptions can prevent the script from crashing when a website is down or when the structure of the webpage changes.
* When reading data from a file, exception handling can be used to deal with file-not-found errors or corrupted data.

</details>
<details><summary>Implementation</summary> 

## Common examples of exceptions include:

### ZeroDivisionError: 
Raised when you attempt to divide a number by zero.

```
try:
    # Code that might raise an exception
    result = 10 / 0
except ZeroDivisionError:
    # Handle the exception
    print("Error: Division by zero is not allowed.")
    result = 0
print("The result is:", result)
```

In this example, the code within the **`try`** block attempts to divide 10 by 0, which will raise a **`ZeroDivisionError`** exception. Instead of allowing the program to crash, the **`except`** block catches the **`ZeroDivisionError`** and handles it gracefully by printing an error message and assigning a default value to the **`result`** variable. The program then continues executing the next line, printing the result.

You can have multiple **`except`** blocks to handle different types of exceptions. Additionally, you can use a **`finally`** block to specify code that should be executed regardless of whether an exception occurred or not, such as closing a file or releasing system resources.

### FileNotFoundError: 
Raised when you try to access a file that doesn't exist.

```
try:
    with open("data.txt", "r") as file:
        data = file.read()
        # Perform calculations on data
        result = calculate(data)
        print("Result:", result)
except FileNotFoundError:
    print("Error: File not found.")
except:
    print("Error: Unable to read the file or perform calculations.")
```

This code is using the **`try`** with multiple **`except`** blocks to handle potential exceptions that may occur when working with files and performing calculations.

*The **`try`** block:*

* It attempts to open the file `data.txt` in read mode using the **`with`** statement, which ensures that the file is properly closed after the block is executed, even if an exception occurs.
* If the file is opened successfully, it reads the contents of the file into the **`data`** variable.
* It then performs some calculations on the **`data`** using a function called **`calculate(data)`**, and the result is stored in the **`result`** variable.
* Finally, it prints the **`result`**.

*The first **`except`** block:*
* This block catches the **`FileNotFoundError`** exception, which is raised when the file `data.txt` is not found in the specified location.
* If a **`FileNotFoundError`** occurs, it prints the error message "Error: File not found."

*The second **`except`** block:*
* This block is a general **`except`** clause that catches any other exception that might occur during the execution of the code inside the **`try`** block.
* If any exception other than **`FileNotFoundError`** occurs, such as an error reading the file or an issue during the calculations, it prints the error message "Error: Unable to read the file or perform calculations."

### ValueError: 
Raised when a function receives an argument of the correct type but an inappropriate value.

try:
    # Code that might raise exceptions
    num1 = int(input("Enter the first number: "))
    num2 = int(input("Enter the second number: "))

    result = num1 / num2

except ValueError:
    print("Error: Invalid input. Please enter a valid integer.")

except ZeroDivisionError:
    print("Error: Cannot divide by zero.")

else:
    # Executed if no exceptions were raised in the try block
    print(f"The result of {num1} / {num2} is: {result}")

finally:
    # Executed regardless of whether an exception occurred or not
    print("This will always be executed.")

print("Program execution continues...")

* In the **`try`** block, we prompt the user to enter two numbers using the **`input`** function. We then attempt to convert the input strings to integers using the **`int()`** function.
* If the user enters an invalid input (e.g., a non-integer value), a **`ValueError`** exception will be raised because the **`int()`** function expects a valid integer string as input. The corresponding **`except`** block will catch this exception and print an error message.
* If the user enters a valid integer for the second number **`num2`**, but it happens to be zero, a **`ZeroDivisionError`** exception will be raised when we attempt to divide **`num1`** by **`num2`**. The second **`except`** block will catch this exception and print an error message.
* The **`else`** block will be executed only if no exceptions were raised in the **`try`** block. In this case, it will print the result of the division operation.
* The **`finally`** block will always be executed, regardless of whether an exception occurred or not. In this example, it prints the message "This will always be executed."
* After the **`try-except-else-finally`** block, the program execution continues with the next line, printing "Program execution continues..."

#### Here's an example run:

Enter the first number: 10  
Enter the second number: 0  
Error: Cannot divide by zero.  
This will always be executed.  
Program execution continues...

In this run, a **`ZeroDivisionError`** occurred, so the corresponding **`except`** block was executed, and the **`else`** block was skipped. However, the **`finally`** block was still executed, and the program continued.

#### Another example run:

Enter the first number: abc  
Error: Invalid input. Please enter a valid integer.  
This will always be executed.  
Program execution continues...

In this run, a **`ValueError`** occurred because the input was not a valid integer, so the corresponding **`except`** block was executed, and both the **`else`** and the division operation were skipped. The **`finally`** block was still executed, and the program continued.

By using multiple **`except`** blocks, you can handle different types of exceptions separately, providing appropriate error messages and actions for each case. The **`else`** block allows you to execute code when no exceptions occur, and the **`finally`** block ensures that certain cleanup or finalization code is always executed, regardless of whether an exception occurred or not.

</details>
<details><summary>Summary</summary> 
<br>

The **`try`** statement is used to enclose the code that might raise an exception, while the **`except`** statement is used to handle the specific exceptions that might occur. If an exception occurs within the **`try`** block, Python looks for the corresponding **`except`** block and executes the code within that block. You can have multiple **`except`** blocks to handle different types of exceptions. The **`else`** clause is executed if no exceptions occur in the **`try`** block, and the **`finally`** clause is always executed, regardless of whether an exception occurred or not, allowing you to perform cleanup or finalization tasks.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)
</details>
