<details><summary>Learning Objectives</summary>
<br>

* Distinguish between integers (`int`), floating-point numbers (`float`), and complex numbers.
* Use basic arithmetic operators (`+`, `-`, `*`, `/`, `%`, `//`) and the exponentiation operator (`**`).
* Employ functions like `round()`, `abs()`, `pow()`, and those within the `math` module.
* Learn to convert types using `int()`, `float()`, and `complex()`.

</details>
<details><summary>Description</summary>
<br> 

Python provides built-in support for working with different kinds of numeric data types: integers, floating-point numbers, and complex numbers.

In Python, numbers are treated as objects, and you can create them directly by assigning literal values to variables, like `x = 10` (`integer`), `y = 3.14` (`float`), or `z = 2 + 3j` (`complex`). Alternatively, Python offers constructor functions `int()`, `float()`, and `complex()` that you can use to create numbers from other data.

Complex numbers, which have a real and an imaginary component, are particularly useful in fields like geometry, calculus, and scientific computing. However, integers and floating-point numbers cover most general numerical use cases. The formula for complex numbers is `x + yj`, where `x` is the real component and `y` is the imaginary part.

It's worth noting that numbers in Python are immutable, meaning you cannot change the value of an existing number. If you reassign a variable to a new numeric value, Python creates a new object in memory.

Furthermore, Python allows you to define your own numeric representations for custom objects by implementing the `__int()`, `__float()`, and `__complex()__` methods. This can be useful when working with specialized data structures or domain-specific problems.

## Types of Python Numbers

There are mainly three types of Python numbers:

* Integer
* Floating-point Numbers/ Decimal point number
* Complex Numbers

## How to Create a Number Variable in Python?

`x = 10`
`y = 12.5`
`z = 1 + 2j`

The complex number has two parts: **real** and **imaginary**. The imaginary part is denoted with a “j” suffix.

## How to find the type of a Number?

We can find the type of a number using the `type()` function.

`x = 10`
`y = 12.5`
`z = 1 + 2j`

```
print(type(x))
print(type(y))
print(type(z))
```

Output:

```
<class 'int'>
<class 'float'>
<class 'complex'>
```

## Changing the data type of Numbers:

Type conversion in Python refers to the process of converting data from one type to another. There are two main types of type conversion:

1. **Implicit Type Conversion:** This is where Python automatically converts one data type to another if the operation being performed is compatible with both types. For example, when you perform arithmetic operations on an integer and a float, Python implicitly converts the integer to a float to complete the calculation.

We can use operations like addition and subtraction to change the type of number implicitly. In simple words, it automatically converts one data type to another.

```
num1 = 10
num2 = 5.0
print(num1 + num2)  # Output: 15.0
```

Here, as you can see, when adding `num1` (`integer`) and `num2` (`float`), the output is automatically converted to a `float`.

2. **Explicit Type Conversion (Typecasting):** In this case, the programmer manually converts one data type to another using built-in functions like `int()`, `float()`, and `complex()`. This process is also known as typecasting.

Python provides built-in functions to explicitly convert between data types. These include:

* `int()` to convert to an integer
* `float()` to convert to a float
* `complex()` to convert to a complex number

When you use these functions and pass a value of a different data type, Python attempts to convert it to the desired type. For instance:

```
num_str = "10"
num_int = int(num_str)  # Converting string to integer

num_float = 3.14
num_int = int(num_float)  # Converting float to integer (truncates decimal part)

num_complex = 2 + 3j
# num_float = float(num_complex)  # Error: Cannot convert complex to float
```

It's important to note that not all type conversions are possible or meaningful. For example, you cannot convert a complex number to an integer or float directly. Additionally, when converting from `float` to `int`, the decimal part is truncated.

Explicit type conversion allows you to have better control over data types in your program and can help prevent certain errors or unintended behavior.

## PEMDAS:

Mathematical operations do not strictly follow the PEMDAS (Parentheses, Exponents, Multiplication, Division, Addition, Subtraction) order of operations that is commonly taught in basic mathematics. Instead, Python follows a specific order of operations known as the Python operator precedence.

The order of operations in Python is as follows:

1. Parentheses
2. Exponentiation (`**`) (right-to-left)
3. Multiplication, Division, Modulus, and Floor Division (`*`, `/`, `%`, `//`) (left-to-right)
4. Addition and Subtraction (`+`, `-`) (left-to-right)

Here are a few key differences from the PEMDAS order:

* Exponentiation is evaluated from right to left, rather than left to right.
* Multiplication, division, modulus, and floor division have the same precedence and are evaluated from left to right.
* There is no separate precedence level for multiplication and division.

For example, consider the following expression:

`2 + 3 * 4 ** 2`

In Python, this expression will be evaluated as follows:

1. `4 ** 2` is evaluated first (right-to-left), resulting in 16.
2. `3 * 16` is evaluated next (left-to-right), resulting in 48.
3. `2 + 48` is evaluated last (left-to-right), resulting in 50.

So, the final result of this expression in Python is `50`.

If you want to override the default operator precedence, you can use parentheses to explicitly group operations and control the order of evaluation.

It's important to note that while Python's operator precedence differs slightly from the traditional PEMDAS order, it is consistent and well-defined. As long as you are aware of Python's specific order of operations, you can write correct mathematical expressions in your code.

</details>
<details><summary>Real World Application</summary>
<br>

Numbers are the backbone of countless Python applications. Here are a few examples:

* **Scientific Calculations:** Performing complex physics simulations, engineering computations, or statistical analyses.
* **Financial Modeling:** Building stock price analysis tools, budgeting applications, or investment calculators.
* **Game Development:** Calculating character positions, scores, and handling in-game physics.
* **Data Science and Machine Learning:** Representing and manipulating numerical data, essential for algorithms and models.

</details>
<details><summary>Implementation</summary> 

## INTEGER:

In Python, integers are zero, positive, or negative whole numbers without a fractional part and having unlimited precision, e.g., 0, 100, -10. The following are valid integer literals in Python.

```
# Integer variables
x = 0
print(x)

x = 100
print(x)

x = -10
print(x)

x = 1234567890
print(x)

x = 5000000000000000000000000000000000000000000000000000000
print(x)
```

Integers can be **binary** - A number having `0b` with digits in the combination of 0 and 1 represents binary numbers, **octal** - A number having `0o` or `0O` as a prefix represents an octal number, and **hexadecimal values** - A number with `0x` or `0X` as a prefix represents a hexadecimal number.

```
b = 0b11011000  # binary
print(b)

o = 0o12  # octal
print(o)

h = 0x12  # hexadecimal
print(h)
```

**Note:** Leading zeros in non-zero integers are not allowed in Python, e.g., `000123` is an invalid number and `0000` becomes 0.

```
x = 001234567890  # SyntaxError: invalid token
```

Python does not allow a comma as a number delimiter. Use underscore `_` as a delimiter instead.

```
x = 1_234_567_890
print(x)  # Output: 1234567890
```

Note that integers must be without a fractional part (decimal point). If it includes a fraction, then it becomes a float.

```
x = 5
print(type(x))  # Output: <class 'int'>

x = 5.0
print(type(x))  # Output: <class 'float'>
```

The `int()` function converts a string or float to an int.

```
x = int('100')
print(x)  # Output: 100

y = int('-10')
print(y)  # Output: -10

z = int(5.5)
print(z)  # Output: 5

n = int('100', 2)
print(n)  # Output: 4
```

## FLOAT:

In Python, floating-point numbers (`float`) are positive and negative real numbers with a fractional part denoted by the decimal symbol `.` or the scientific notation `E` or `e`, e.g., 1234.56, 3.142, -1.55, 0.23.

```
f = 1.2
print(f)  # Output: 1.2
print(type(f))  # Output: <class 'float'>

f = 123_42.222_013  # Output: 12342.222013
print(f)

f = 2e400
print(f)  # Output: inf
```

As you can see, a floating-point number can be separated by the underscore `_`. The maximum size of a float depends on your system. The float beyond its maximum size is referred to as `inf`, `Inf`, `INFINITY`, or `infinity`. For example, a float number `2e400` will be considered as infinity for most systems.

Scientific notation is used as a short representation to express floats with many digits. For example: `345.56789` is represented as `3.4556789e2` or `3.4556789E2`.

```
f = 1e3
print(f)  # Output: 1000.0

f = 1e5
print(f)  # Output: 100000.0

f = 3.4556789e2
print(f)  # Output: 345.56789
print(type(f))  # Output: <class 'float'>
```

Use the `float()` function to convert a string to a float.

```
f = float('5.5')
print(f)  # Output: 5.5

f = float('5')
print(f)  # Output: 5.0

f = float('     -5')
print(f)  # Output: -5.0

f = float('1e3')
print(f)  # Output: 1000.0

f = float('-Infinity')
print(f)  # Output: -inf

f = float('inf')
print(f)  # Output: inf
print(type(f))  # Output: <class 'float'>
```

## Complex Numbers

A complex number is a number with real and imaginary components. For example, `5 + 6j`
is a complex number where 5 is the real component and 6 multiplied by j is an imaginary component.

 a = 5 + 2j
 print(a)
 print(type(a))

You must use j or J as the imaginary component. Using other characters will throw a syntax error.

 a = 5 + 2k
 a = 5 + j
 a = 5i + 2j

## Type Conversion:

The following is an example of converting the numbers from one type to another:

 a = 10 # int

 b = 31.54 # float

 c = 3j # complex

 # convert from int to float
 x = float(a)

 # convert from float to int
 y = int(b)

 # convert from float to complex
 z = complex(b)

 print(x)
 print(y)
 print(z)

 print("x type: ", type(x))
 print("y type: ", type(y))
 print("z type: ", type(z))

Output:

 10.0
 31
 (31.54+0j)
 x type: <class 'float'>
 y type: <class 'int'>
 z type: <class 'complex'>

If you observe the above result, we converted numbers from __int__ to __float__, __float__ to __int__, and __float__ to __complex__ types.

Here, you need to remember that it’s impossible to convert complex numbers into another type in Python.

## Arithmetic Operators using Numbers:

Let's go through the code and explain the operations using the PEMDAS (Parentheses, Exponents, Multiplication, Division, Addition, Subtraction) order of operations.

 a, b = 10, 20

This line assigns the values 10 and 20 to the variables a and b, respectively.

 print("a + b =", a + b)

 # Output: a + b = 30

According to PEMDAS, addition (+) is the last operation to be performed. So, the values of a and b are first substituted (10 + 20), and then the addition is performed, resulting in 30.

 print("a - b =", a - b)

 # Output: a - b = -10

Similar to addition, subtraction (-) is also one of the last operations in PEMDAS. The values of a and b are substituted (10 - 20), and then the subtraction is performed, resulting in -10.

 print("b - a =", b - a)

 # Output: b - a = 10

Following PEMDAS, the values of b and a are substituted (20 - 10), and then the subtraction is performed, resulting in 10.

 print("a * b =", a * b)

 # Output: a * b = 200

According to PEMDAS, multiplication (*) has higher precedence than addition and subtraction. The values of a and b are substituted (10 * 20), and then the multiplication is performed, resulting in 200.

 print("b / a =", b / a)

 # Output: b / a = 2.0

Division (/) has the same precedence as multiplication in PEMDAS. The values of b and a are substituted (20 / 10), and then the division is performed, resulting in 2.0.

 b = 22
 print("b % a =", b % a)

 # Output: b % a = 2

The value of b is reassigned to 22. The modulus operator (%) has the same precedence as multiplication and division in PEMDAS. The values of b and a are substituted (22 % 10), and then the modulus operation is performed, resulting in 2.

 a = 3
 print("a ** 3 =", a ** 3)

 # Output: a ** 3 = 27

According to PEMDAS, exponentiation (**) has higher precedence than multiplication, division, addition, and subtraction. The value of a is reassigned to 3. The exponentiation operation is performed (3 ** 3), resulting in 27.

 a, b = 9, 2
 print("a // b =", a // b)

 # Output: a // b = 4

The values of a and b are reassigned to 9 and 2, respectively. The floor division operator (//) has the same precedence as multiplication, division, and modulus in PEMDAS. The values of a and b are substituted (9 // 2), and then the floor division is performed, resulting in 4.

The PEMDAS order of operations is followed throughout the code, with parentheses being evaluated first, followed by exponents, then multiplication and division (from left to right), and finally, addition and subtraction (from left to right).

## Using Built-in Functions:

* __Pow():__ The pow() function takes two parameters and returns the first parameter raised to the power of the second. If x and y are parameters, the result of the pow() function is x raised to the power of y. The parameters can be of any numeric type.

 print(pow(10, 2)) # output: 100

 print(pow(100, 0.5)) # output: 10.0

 print(pow(25, -2)) # output: 0.04

 print(pow(10, -2)) # output: 0.01

 print(pow(100, 2 + 0j)) # output: (10000 + 0j)

* __abs():__ The abs() function returns the absolute value of a number without considering its sign. In other words, the absolute value of a number will always return a positive number. The function can have any numeric object as a parameter. If it is a complex number, its magnitude is returned. (Magnitude of a + bj is (a^2 + b^2)^(1/2))

 print(abs(-10)) # output: 10

 print(abs('10'))

 print(abs(-1.5)) # output: 1.5

 print(abs(1 + 2j)) # output: 2.23606797749979 # this is sqrt(5)

* __round():__ The round() function returns a number rounded to the specified position after the decimal point.

 print(round(1234.456, 2)) # output: 1234.46

 print(round(1234.456, 1)) # output: 1234.5

 print(round(1234.456, 0)) # output: 1234.0

 print(round(1234.456, -1)) # output: 1230.0

* __random():__ 

 __Syntax:__

 random.randint(a, b)

This returns a random number N within the range of a and b (a <= N <= b), where a and b are included within the range.

Here’s an example:

Build a dice game – a program that generates a random number between 0 and 6 each time you run the code.

 # importing the random module

 import random 
 print(random.randint(0, 6))

Output:

 5

__Note:__ Every time you execute the above code, the output would be different in a range of 0 to 6. That’s just how we roll the dice. 

* __math():__

Let’s see the following example:

 # importing pre-defined math module 
 import math

 print(math.pi)

 print(math.cos(math.pi))

 print(math.exp(10))

 print(math.log10(1000))

 print(math.sinh(1))
 
 print(math.factorial(6))

</details>
<details><summary>Summary</summary>
<br>

* Python provides flexible numeric types to represent different kinds of numbers.
* Arithmetic operations and mathematical functions enable you to perform calculations.
* Number conversions allow you to work with different types interchangeably.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
