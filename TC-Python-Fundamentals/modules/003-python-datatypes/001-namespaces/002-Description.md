# Introduction

# What are Namespaces in Python?
All variables in Python exist in a namespace: the namespace the variable exists in determines what resources can and can't interact with that variable. There are four name spaces in Python
- Built-In
- Global
- Local
- Enclosing

# Built-In Namespace
All variables, classes, functions, etc. that are built-in to Python exist in the "Built-In" scope (int, str, list len, print, input, etc.). These resources can be referenced anywhere in your code and should not have their values changed.

# Global Namespace
Any reference you create directly in the module exists in the Global namespace: these are the resources that can be exported into other modules in your application. An easy way to check if a variable exists in the global scope is to check its indentation: if there is no tab or space before the reference then it exists in the Global namespace

# Local Namespace
The Local namespace is any block of nested code inside a class or function. Anything defined in this "local" space exists only within the space and can't be referenced outside that nested space directly.

# Enclosing Namespace
Anytime you have a function defined within another function you create an Enclosing namespace: The Local namespace of the outer function is available to the inner function, but not vice versa. 