# Cumulative for Namespaces

<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:

- Define the four namespaces of Python

</details>

<details><summary>Description</summary>

# Introduction

# What are Namespaces in Python?
All variables in Python exist in a namespace: the namespace the variable exists in determines what resources can and can't interact with that variable. There are four namespaces in Python:
- Built-In
- Global
- Local
- Enclosing

# Built-In Namespace
All variables, classes, functions, etc. that are built-in to Python exist in the "Built-In" scope (int, str, list, len, print, input, etc.). These resources can be referenced anywhere in your code and should not have their values changed.

# Global Namespace
Any reference you create directly in the module exists in the Global namespace: these are the resources that can be exported into other modules in your application. An easy way to check if a variable exists in the global scope is to check its indentation: if there is no tab or space before the reference, then it exists in the Global namespace.

# Local Namespace
The Local namespace is any block of nested code inside a class or function. Anything defined in this "local" space exists only within that space and can't be referenced outside that nested space directly.

# Enclosing Namespace
Anytime you have a function defined within another function, you create an Enclosing namespace: The Local namespace of the outer function is available to the inner function, but not vice versa.  
</details>
<details><summary>Real World Application</summary>

# Real World Application forNamespaces
Namespaces are useful for keeping your code organized and modular. In smaller projects, you can leverage the namespaces to control access to resources in your code, and in larger projects, the namespaces allow you to avoid naming conflicts and share resources across modules where necessary.

Keep in mind that whatever the scope of your code, you will need to know how the namespaces interact and how to access resources in them to ensure your code functions properly.

</details>
<details><summary>Implementation</summary> 

# Implementation

## Built-In Namespace
```python
# Anything that comes pre-provided by Python exists in the Built-In namespace
print("Hello Built-In namespace!")
```

## Global Namespace
Module One
```python
# Because this variable is defined directly in the module, it exists in the Global namespace
# This means we can export it into another module
person_name = "Billy"
```
Module Two
```python
# This will import the "person_name" variable into the module and print its value to the terminal
# We can do this because the variable exists in the Global namespace
from module_one import person_name
print(person_name)
```

## Local Namespace
```python
def double_number(num):
    # This variable exists only in the Local namespace of the function
    doubler = 2
    return num * doubler

print(doubler)  # this will give you a NameError, since doubler is not defined outside the Local
                  # namespace of the function 
```

## Enclosing Namespace
```python
def doubler_function(num):
    # because we have an inner function, this doubler function exists in the Enclosing namespace
    doubler = 2
    def multiplier_function():
        # The inner function has access to the enclosing space of the function in which it is defined
        result = num * doubler
        return result
    # because the doubler_function does not have access to the Local namespace of the
    # multiplier_function we have to call the multiplier_function to gain access to "result"
    return multiplier_function()
```

</details>
<details><summary>Summary</summary> 

# Summary
Python namespaces determine where data can be accessed.

- Built In: the resources built into the language exist in the Built-In namespace and can be accessed anywhere in your code.
- Global: the resources built directly into your modules can be accessed anywhere in your module and can be imported by other modules.
- Local: resources created within a class or function cannot be accessed outside of the class/function directly.
- Enclosing: resources in a function can be accessed by any functions defined within the outer function.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
