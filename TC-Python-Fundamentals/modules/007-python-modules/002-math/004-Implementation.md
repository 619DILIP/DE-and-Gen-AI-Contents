# Implementation 

## Accessing the Math Module Content
To make use of the math module you first have to import it into your module
```python
import math
```
This will give you access to all the functions it contains; if you only need a few specific functions you can import them instead of the whole module
```python
from math import factorial
```

## Curated Collection of Math Features
```python
import math

# rounds a number up to the nearest integer
ceil_result = math.ceil(4.3)
print(f"Ceiling of 4.3 is: {ceil_result}")  # Output: Ceiling of 4.3 is: 5

# rounds a number down to the nearest integer
floor_result = math.floor(4.8)
print(f"Floor of 4.8 is: {floor_result}")  # Output: Floor of 4.8 is: 4

# returns the square root of a number
sqrt_result = math.sqrt(16)
print(f"Square root of 16 is: {sqrt_result}")  # Output: Square root of 16 is: 4.0

# returns the result of raising a number to the power
pow_result = math.pow(2, 3)
print(f"2 raised to the power of 3 is: {pow_result}")  # Output: 2 raised to the power of 3 is: 8.0

# represents the value of pi
pi_value = math.pi
print(f"Value of pi is: {pi_value}")  # Output: Value of pi is: 3.141592653589793
```
