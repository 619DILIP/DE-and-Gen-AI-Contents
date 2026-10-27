# Introduction 

Python provides built-in support for working with different kinds of numeric data types - integers, floating-point numbers, and complex numbers. 

In Python, numbers are treated as objects, and you can create them directly by assigning literal values to variables, like x = 10 (integer), y = 3.14 (float), or z = 2 + 3j (complex). Alternatively, Python offers constructor functions int(), float(), and complex() that you can use to create numbers from other data.

Complex numbers, which have a real and imaginary component, are particularly useful in fields like geometry, calculus, and scientific computing. However, integers and floating-point numbers cover most general numerical use cases. The formula for complex numbers is x + yj, where x is the real component and y is the imaginary part.

It's worth noting that number objects in Python are immutable, meaning you cannot change the value of an existing number. If you reassign a variable to a new numeric value, Python creates a new object in memory.

Furthermore, Python allows you to define your own numeric representations for custom objects by implementing the __int(), float(), and complex()__ methods. This can be useful when working with specialized data structures or domain-specific problems.

## Types of Python Number

There are mainly three types of Python Number:

* Integer
* Floating-point Numbers/ Decimal point number
* Complex Numbers

## How to Create a Number Variable in Python?

        x = 10;
        y = 12.5;
        z = 1 + 2j

The complex number has two parts – __real__ and __imaginary__. The imaginary part is denoted with “j” suffix.

## How to find the type of a Number?

We can find the type of number using the __type()__ function.

        x = 10;
        y = 12.5;
        z = 1 + 2j

        print(type(x))
        print(type(y))
        print(type(z))

Output:

        <class 'int'>
        <class 'float'>
        <class 'complex'>


## Changing the data type of Numbers:

Type conversion in Python refers to the process of converting data from one type to another. There are two main types of type conversion:

1. __Implicit Type Conversion:__ This is where Python automatically converts one data type to another if the operation being performed is compatible with both types. For example, when you perform arithmetic operations on an integer and a float, Python implicitly converts the integer to a float to complete the calculation.

Here's how explicit type conversion or typecasting works with examples:

We can use operations like addition, subtraction to change the type of number implicitly. In simple words, automatically converts one data type to another. 

        num1 = 10 
        num2 = 5.0 
        print (num1 + num2)

        # Output: 15.0

Here as you can see, on adding num1(integer) and num2(float), the output is automatically converted to a float type.  

2. __Explicit Type Conversion (Typecasting):__ In this case, the programmer manually converts one data type to another using built-in functions like int(), float(), and complex(). This process is also known as typecasting.

Here's how explicit type conversion or typecasting works with examples:

Python provides built-in functions to explicitly convert between data types. These include:

* __int()__ to convert to an integer
* __float()__ to convert to a float
* __complex()__ to convert to a complex number

When you use these functions and pass a value of a different data type, Python attempts to convert it to the desired type. For instance:

        num_str = "10"
        num_int = int(num_str)  # Converting string to integer

        num_float = 3.14
        num_int = int(num_float)  # Converting float to integer (truncates decimal part)

        num_complex = 2 + 3j
        num_float = float(num_complex)  # Error: Cannot convert complex to float

It's important to note that not all type conversions are possible or meaningful. For example, you cannot convert a complex number to an integer or float directly. Additionally, when converting from float to int, the decimal part is truncated.

Explicit type conversion allows you to have better control over data types in your program and can help prevent certain errors or unintended behavior.

## PEMDAS:

Mathematical operations do not strictly follow the PEMDAS (Parentheses, Exponents, Multiplication, Division, Addition, Subtraction) order of operations that is commonly taught in basic mathematics. Instead, Python follows a specific order of operations known as the Python operator precedence.

The order of operations in Python is as follows:

1. Parentheses
2. Exponentiation (**) (right-to-left)
3. Multiplication, Division, Modulus, and Floor Division (*, /, %, //) (left-to-right)
4. Addition and Subtraction (+, -) (left-to-right)

Here are a few key differences from the PEMDAS order:

* Exponentiation is evaluated from right to left, rather than left to right.
* Multiplication, division, modulus, and floor division have the same precedence and are evaluated from left to right.
* There is no separate precedence level for multiplication and division.

For example, consider the following expression:

        2 + 3 * 4 ** 2

In python, this expression will be evaluated as follows:

1. __`4 ** 2`__ is evaluated first (right-to-left), resulting in 16.
2. __`3 * 16`__ is evaluated next (left-to-right), resulting in 48.
3. __`2 + 48`__ is evaluated last (left-to-right), resulting in 50.

So, the final result of this expression in Python is __`50`__.

If you want to override the default operator precedence, you can use parentheses to explicitly group operations and control the order of evaluation.

It's important to note that while Python's operator precedence differs slightly from the traditional PEMDAS order, it is consistent and well-defined. As long as you are aware of Python's specific order of operations, you can write correct mathematical expressions in your code.
