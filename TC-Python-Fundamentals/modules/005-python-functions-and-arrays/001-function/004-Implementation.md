<details><summary>Implementation</summary>
<br>
Functions in are versatile tools that can be used for a wide range of tasks. Let's explore some common types of functions and their implementations:

### Basic Function with Parameters:
```py
def greet(name):
    return f"Hello, {name}!"
    
message = greet("John")
print(message)  # Output: Hello, John!
```

* A function named `greet` is defined that takes a parameter `name`. 
* Inside the function, it uses an `f`-string (formatted string literal) to create a greeting message with the input name. 
* For example, if the input name "John," is passed into the greet method the returned message will be "Hello, John!".

* When we say greet(”John”) we are telling the compiler to pass the value of “John” in for our parameter name of the greet method. 

* An `f-string` is a string prefixed with the letter `f`, and it allows you to embed Python expressions directly inside the string.
* The function is then called with the argument "John", and the returned greeting message is stored in the variable message.
* Finally, the code uses the `print()` function to output the value of the message variable, which will be "Hello, John!" in this case.

### Function with Default Parameters:
```py
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"
message1 = greet("John")
message2 = greet("Jane", "Hi")
print(message1)  # Output: Hello, John!
print(message2)  # Output: Hi, Jane!
```
* A function named `greet` is defined that takes two parameters: `name` and `greeting`, with the greeting parameter having a default value of "Hello". Inside the function, it uses an `f-string` to create a greeting message using the provided greeting and name.

* The function is then called with the argument "John" for name, and since no greeting argument is provided, it uses the default greeting "Hello". The returned message is stored in the variable message1.

* Calling the function with custom argument: Next, the function is called with the arguments "Jane" for name and "Hi" for greeting. The returned message is stored in the variable message2.

* Finally, the print() function is used to output the values of message1 and message2, which will be "Hello, John!" and "Hi, Jane!" respectively.


### Function with Variable Number of Arguments (*args):
```py
def sum_numbers(*args):
    total = 0
    for num in args:
        total += num
    return total
result = sum_numbers(1, 2, 3, 4, 5)
print(result)  # Output: 15
```
* The `sum_numbers()` function takes any number of arguments using `*args`.

* Inside the function, a variable named `total` is initialized to 0.

* It then iterates over each number in the provided arguments (`args`) and adds them to the `total` variable, which is then returned.

* The `sum_numbers()` is called with the following arguments `(1, 2, 3, 4, 5)` which is stored in a variable called `results`.

* Finally, the `result` is printed out with the output of 15.


### Function with Keyword Arguments (**kwargs):
```py
def display_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")
display_info(name="John", age=30, city="New York")
# Output:
# name: John
# age: 30
# city: New York
```

* The `display_info()` accepts keyword arguments using `**kwargs`. 
* The `**kwargs` syntax allows passing any number of keyword arguments to the function.
* `for key, value in kwargs.items()`:
This for loop iterates over the items (key-value pairs) in the kwargs dictionary.
* `print(f"{key}: {value}")`
Inside the loop, it prints each key-value pair in the format key: value.
* `display_info(name="John", age=30, city="New York")`:
This line calls the display_info function with three keyword arguments: name="John", age=30, and city="New York".

### Recursive Function (Factorial Example):

* Recursion refers to the concept of a function calling itself within its own definition. 

* This technique allows a function to solve complex problems by breaking them down into smaller, similar sub-problems. 

* In recursion, the function continues calling itself with modified arguments until it reaches a base case, which is a condition that stops the recursive calls.

#### Example: 
```py
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)

result = factorial(5)
print(result)  # Output: 120
```

* The `factorial()` accepts one parameter `n`.
* Inside the `factorial()` a conditional statement is used to check if `n` is equal to 0.
* If `n` equals to 0, then the function returns 1, This is the base case for the factorial function because factorial of 0 is defined as 1.
* If `n` not equal to 0, then it recursively calculates the factorial.
* Them then factorial of 5 is calculated and stored in the variable `result`.
* Finally `result` is printed out which gives us the factorial of 5, which is 120. 

### Higher-Order Function (Function as Parameter):
```py
def apply_operation(operation, x, y):
    return operation(x, y)
def add(a, b):
    return a + b
def multiply(a, b):
    return a * b
result1 = apply_operation(add, 3, 5)
result2 = apply_operation(multiply, 3, 5)
print(result1)  # Output: 8
print(result2)  # Output: 15 
```

* `def apply_operation(operation, x, y)`:
This line defines a function named `apply_operation()` that takes three parameters: `operation`, `x`, and `y`.

* Inside the function, it calls the operation function with arguments `x` and `y`and returns the result.
* `def add(a, b)`:
This line defines a function named `add()` that takes two parameters `a` and `b`.

* Inside the function, it returns the sum of `a` and `b`.

* `def multiply(a, b)`:
This line defines a function named `multiply()` that takes two parameters `a` and `b`.

* Inside the function, it returns the product of `a` and `b`.

* `result1 = apply_operation(add, 3, 5)`:

* This line calls the `apply_operation()` function with the `add()` function as the operation argument and 3 and 5 as the x and y arguments, respectively.
*  It calculates the sum of 3 and 5, resulting in result1 being 8.

* `result2 = apply_operation(multiply, 3, 5)`:

* This line calls the `apply_operation function()` with the `multiply()` function as the operation argument and 3 and 5 as the x and y arguments, respectively.
* It calculates the product of 3 and 5, resulting in result2 being 15.
* `print(result1) and print(result2)`:
* Finally, these lines print the values of result1 and result2, which are 8 and 15, respectively.

</details>