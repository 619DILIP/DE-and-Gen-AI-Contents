# Cumulative for the math
<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:

- Explain what the "math" module is used for
- describe some common functions and their uses in the "math" module

</details>

<details><summary>Description</summary>

# Introduction 
The math module in Python is part of the standard library; it provides programmers with a collection of mathematical functions and constants that facilitate various calculations. These functions cover a wide range of mathematical operations, from computing square roots to performing combinatorial calculations. Additionally, the module provides essential constants like π (pi) and e (Euler's number). When working on mathematical tasks within Python, developers can import the math module to access these features.

</details>
<details><summary>Real World Application</summary>

# Real World Application for the Math Module
Much of programming involves making one or more computers perform mathematical calculations for us, and then taking one or more actions based on the results of those calculations. As the Python language has developed, common algorithms and mathematical functions have been recognized and implemented in the math module for ease of use. Whether you are working on a coding challenge or trying to optimize your code base, the functions and constants provided in the math module are typically more than sufficient for handling your use case.

Should you find yourself needing more functionality or more optimized solutions for your mathematical operations, there is likely to be a third-party package of code that has a solution you can use, and more likely than not, that package will make use of the math module.

</details>
<details><summary>Implementation</summary> 

# Implementation 

## Accessing the Math Module Content
To make use of the math module, you first have to import it into your module
`import math`
This will give you access to all the functions it contains; if you only need a few specific functions, you can import them instead of the whole module
`from math import factorial`

## Curated Collection of Math Features
`import math`

# rounds a number up to the nearest integer
`ceil_result = math.ceil(4.3)`
`print(f"Ceiling of 4.3 is: {ceil_result}")`  # Output: Ceiling of 4.3 is: 5

# rounds a number down to the nearest integer
`floor_result = math.floor(4.8)`
`print(f"Floor of 4.8 is: {floor_result}")`  # Output: Floor of 4.8 is: 4

# returns the square root of a number
`sqrt_result = math.sqrt(16)`
`print(f"Square root of 16 is: {sqrt_result}")`  # Output: Square root of 16 is: 4.0

# returns the result of raising a number to a given power
`pow_result = math.pow(2, 3)`
`print(f"2 raised to the power of 3 is: {pow_result}")`  # Output: 2 raised to the power of 3 is: 8.0

# represents the value of pi
`pi_value = math.pi`
`print(f"Value of pi is: {pi_value}")`  # Output: Value of pi is: 3.141592653589793

</details>
<details><summary>Summary</summary> 

# Summary 
- The math module contains functions and constants for performing common mathematical operations.
- The entire module can be imported for quick access to all the features.
- Individual functions and constants can be imported if you know the specific features needed for your code.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
