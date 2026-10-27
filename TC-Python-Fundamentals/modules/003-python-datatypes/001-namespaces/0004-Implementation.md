# Implementation

## Built-In Namespace
```python
# anything that comes pre-provided by Python exists in the Built-In namespace
print("Hello Built-In namespace!")
```

## Global Namespace
Module One
```python
# Because this variable is defined directly in the module it exists in the Global namespace
# This means we can export it into another module
person_name = "Billy
```
Module Two
```python
# this will import the "person_name" variable into the module and print its value to the terminal
# we can do this because the variable exists in the Global namespace
from module_one import person_name
print(person_name)
```

## Local Namespace
```python
def double_number(num):
    # this variable exists only in the Local namespace of the function
    doubler = 2
    return num * doubler
print(doubler) # this will give you a NameError, since doubler is not defined outside the Local
               # namespace of the function 
```

## Enclosing Namespace
```python
def doubler_function(num):
    # because we have an inner function this doubler function exists in the Enclosing namespace
    doubler = 2
    def multiplier_function():
        # the inner function has access to Enclosing space of the function it is being defined in
        result = num * doubler
        return result
    # because the doubler_function does not have access to the Local namespace of the 
    # multiplier_function we have to call the multiplier_function to gain access to "result"
    return multiplier_function()
```