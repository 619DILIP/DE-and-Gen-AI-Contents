# Implementation

## Common examples of exceptions include:

### ZeroDivisionError: 
Raised when you attempt to divide a number by zero.

    try:
        # Code that might raise an exception
        result = 10 / 0

    except ZeroDivisionError:
        # Handle the exception
        print("Error: Division by zero is not allowed.")
        result = 0

    print("The result is:", result)

In this example, the code within the **`try`** block attempts to divide 10 by 0, which will raise a **`ZeroDivisionError`** exception. Instead of allowing the program to crash, the **`except`** block catches the **`ZeroDivisionError`** and handles it gracefully by printing an error message and assigning a default value to the **`result`** variable. The program then continues executing the next line, printing the result.

You can have multiple **`except`** blocks to handle different types of exceptions. Additionally, you can use a **`finally`** block to specify code that should be executed regardless of whether an exception occurred or not, such as closing a file or releasing system resources.


### FileNotFoundError: 
Raised when you try to access a file that doesn't exist.

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

This code is using the **`try`** with multiple **`except`** blocks to handle potential exceptions that may occur when working with files and performing calculations.

*The **`try`** block:*
  * It attempts to open the file "data.txt" in read mode using the **`with`** statement, which ensures that the file is properly closed after the block is executed, even if an exception occurs.
  * If the file is opened successfully, it reads the contents of the file into the **`data`** variable.
  * It then performs some calculations on the **`data`** using a function called **`calculate(data)`**, and the result is stored in the **`result`** variable.
  * Finally, it prints the **`result`**.

*The first **`except`** block:*
  * This block catches the **`FileNotFoundError`** exception, which is raised when the file "data.txt" is not found in the specified location.
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