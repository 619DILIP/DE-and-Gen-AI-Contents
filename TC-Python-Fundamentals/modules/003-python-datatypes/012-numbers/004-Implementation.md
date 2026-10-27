# Implementation 

## INTEGER:

In Python, integers are zero, positive or negative whole numbers without a fractional part and having unlimited precision, e.g. 0, 100, -10. The followings are valid integer literals in Python.

        #integer variables
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

Integers can be __binary__ - A number having __0b__ with eight digits in the combination of 0 and 1 represent the binary numbers, __octal__ - A number having __0o or 0O__ as prefix represents an octal number, and __hexadecimal values__ - A number with __0x or 0X__ as prefix represents hexadecimal number. 

        b = 0b11011000 # binary
        print(b)

        o = 0o12 # octal
        print(o)

        h = 0x12 # hexadecimal
        print(h)

__Note:__ Leading zeros in non-zero integers are not allowed in Python, e.g. 000123 is invalid number and 0000 becomes 0.

        x=001234567890 #syntaxError: invalid token

Python does not allow comma as number delimiter. Use underscore `_` as a delimiter instead.

        x = 1_234_567_890
        print(x) #output: 1234567890

Note that integers must be without a fractional part (decimal point). It it includes a fractional then it becomes a float.

        x=5
        print(type(x)) #output: <class 'int'>

        x=5.0
        print(type(x)) #output: <class 'float'>

The __int()__ function converts a string or float to int.

        x = int('100')
        print(x) #output: 100

        y = int('-10')
        print(y) #output: -10

        z = int(5.5)
        print(z) #output: 5

        n = int('100', 2)
        print(n) #output: 4



## FLOAT:

In Python, floating point numbers (float) are positive and negative real numbers with a fractional part denoted by the decimal symbol `.` or the scientific notation `E` or `e`, e.g. 1234.56, 3.142, -1.55, 0.23.

        f = 1.2
        print(f) #output: 1.2
        print(type(f)) #output: <class 'float'>

        f=123_42.222_013 #output: 12342.222013
        print(f)

        f=2e400
        print(f) #output: inf

As you can see, a floating point number can be separated by the underscore `_`. The maximum size of a float is depend on your system. The float beyond its maximum size referred as inf, Inf, INFINITY, or infinity. For example, a float number __2e400__ will be considered as infinity for most systems.

Scientific notation is used as a short representation to express floats having many digits. For example: 345.56789 is represented as 3.4556789e2 or 3.4556789E2

        f = 1e3
        print(f) #output: 1000.0

        f = 1e5
        print(f) #output:100000.0

        f = 3.4556789e2
        print(f) #output:
        print(type(f)) #output:345.56789


Use the __float()__ function to convert string, int to float.

        f=float('5.5')
        print(f) #output: 5.5

        f=float('5')
        print(f) #output: 5.0

        f=float('     -5')
        print(f) #output: -5.0

        f=float('1e3')
        print(f) #output: 1000.0

        f=float('-Infinity')
        print(f) #output: -inf

        f=float('inf')
        print(f)  #output: inf
        print(type(f)) #output:<class 'float'>


## Complex Numbers

A complex number is a number with real and imaginary components. For example, __5 + 6j__ is a complex number where 5 is the real component and 6 multiplied by j is an imaginary component.

        a = 5+2j
        print(a)
        print(type(a))

You must use j or J as imaginary component. Using other character will throw syntax error.

        a=5+2k
        a=5+j
        a=5i+2j



## Type Conversion:

Following is the example of converting the numbers from one type to another:

        a = 10 #int

        b = 31.54 #float

        c = 3j #complex

        #convert from int to float
        x = float(a)

        #convert from float to int
        y = int(b)

        #convert from int to complex
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

If you observe the above result, we converted numbers from __int__ to __float__, __float__ to __int__, __int__ to __complex__ types.

Here, you need to remember that it’s impossible to convert complex numbers into another type in python.

## Arithmetic Operators using Numbers:

let's go through the code and explain the operations using the PEMDAS (Parentheses, Exponents, Multiplication, Division, Addition, Subtraction) order of operations.

        a, b = 10, 20

This line assigns the values 10 and 20 to the variables a and b, respectively.

        print("a+b=", a+b)

        # Output: a+b= 30

According to PEMDAS, addition (+) is the last operation to be performed. So, the values of a and b are first substituted (10 + 20), and then the addition is performed, resulting in 30.

        print("a-b=", a-b)

        # Output: a-b= -10

Similar to addition, subtraction (-) is also one of the last operations in PEMDAS. The values of a and b are substituted (10 - 20), and then the subtraction is performed, resulting in -10.

        print("b-a=", b-a)

        # Output: b-a= 10

Following PEMDAS, the values of b and a are substituted (20 - 10), and then the subtraction is performed, resulting in 10.

        print("a*b=", a*b)

        # Output: a*b= 200

According to PEMDAS, multiplication (*) has higher precedence than addition and subtraction. The values of a and b are substituted (10 * 20), and then the multiplication is performed, resulting in 200.

        print("b/a=", b/a)

        # Output: b/a= 2.0

Division (/) has the same precedence as multiplication in PEMDAS. The values of b and a are substituted (20 / 10), and then the division is performed, resulting in 2.0.

        b = 22
        print("b%a=", b%a)

        # Output: b%a= 4

The value of b is reassigned to 22. The modulus operator (%) has the same precedence as multiplication and division in PEMDAS. The values of b and a are substituted (22 % 10), and then the modulus operation is performed, resulting in 4.

        a = 3
        print("a**3=", a**3)

        # Output: a**3= 27

According to PEMDAS, exponentiation (**) has higher precedence than multiplication, division, addition, and subtraction. The value of a is reassigned to 3. The exponentiation operation is performed (3 ** 3), resulting in 27.

        a, b = 9, 2
        print("a//b=", a//b)

        # Output: a//b= 4

The values of a and b are reassigned to 9 and 2, respectively. The floor division operator (//) has the same precedence as multiplication, division, and modulus in PEMDAS. The values of a and b are substituted (9 // 2), and then the floor division is performed, resulting in 4.

The PEMDAS order of operations is followed throughout the code, with parentheses being evaluated first, followed by exponents, then multiplication and division (from left to right), and finally, addition and subtraction (from left to right).

## Using Built-in Functions:

* __Pow():__ The pow() function takes two parameters and returns first parameter raised to second. If x and y are parameters, result of pow() function is x raised to y. The parameters can be of any numeric type.

        print(pow(10,2)) # output: 100

        print(pow(100,0.5)) # output: 10.0

        print(pow(25,-2)) # output: 0.0016

        print(pow(10,-2)) # output: 0.01

        print(pow(100,2+0j)) # output: (10000+0j)

* __abs():__ The abs() returns absolute value of a number without considering its sign. In other words, absolute value of a number will always return a positive number. The function can have any numeric object as parameter. If it is a complex number, its magnitude is returned. (Magnitude of a+bj is a 2+b2)

        print(abs(-10)) # output: 10

        print(abs('10'))

        print(abs(-1.5)) # output: 1.5

        print(abs(1+2j)) # output: 2.23606797749979 #this is 5

* __round():__ The round() function returns a number, rounded to precision of specified position after decimal point.

        print(round(1234.456,2)) # output: 1234.46

        print(round(1234.456,1)) # output: 1234.5

        print(round(1234.456,0)) # output: 1234.0

        print(round(1234.456,-1)) # output: 1230.0

* __random():__ 

__Syntax:__

        random.randint(a,b)

This returns a random number N within the range of a, b (a <= N <= b), where the a, b are included within the range.

Here’s an example:

Build a dice game – A program which generates a random number between 0 and 6 each time you run the code.

        # importing the random module 
   
        import random 
        print(random.randint(0,6))

Output:

        5

__Note:__ Every time you execute the above code the output would be different in a range of 0 to 6. That’s just how we roll the dice. 

* __math():__

Let’s see the following example:

        #importing pre-defined math module 
        import math
 
        print(math.pi)

        print(math.cos(math.pi))

        print(math.exp(10))

        print(math.log10(1000))

        print(math.sinh(1))
        
        print(math.factorial(6))


