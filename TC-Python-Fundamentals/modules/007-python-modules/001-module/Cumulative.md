# Cumulative for the module

<details><summary>Learning Objectives</summary>

# Learning Objectives
After completing this module, associates should be able to:

- Describe what a Python module is
- Describe how Python modules are used

</details>

<details><summary>Description</summary>

# What is a Module
A module is a file in which Python code is written: this can be your file, a file included in the base library, or a third-party package. The most common way of indicating your file is a module is to add the ".py" extension.

This is a useful distinction because your code is not always going to work with other Python modules strictly: sometimes you will need to load data from different files (like a CSV) into your code. So, if for no other reason, using the ".py" extension helps to make obvious which files have your code and which do not.

</details>
<details><summary>Real World Application</summary>

# Real World Application for Modules
Without modules, you can't have Python code: it's as simple as that. Any Python project has to create and manage modules, so it is imperative for any aspiring Python developer to become familiar with how modules work.

For simple Python scripts (think small, one-time jobs you need done now and then), a single module will typically be sufficient. You write the code you need, then execute the module as your script.

If you are building a larger application, you will most likely want to write your code in multiple modules to help keep things organized, using Python's importing abilities to transfer data across modules at runtime. In these situations, you will probably deploy your modules to a virtual computer in the cloud (aka: send the files across the web to a computer you are paying to use that is publicly accessible by others) and start your application in that virtual instance, which will give your users access to the application.

</details>
<details><summary>Implementation</summary>

# Implementation

## Create a Module
To create a module, you simply make a new file and make sure to give it the ".py" extension. The common convention when creating modules is to use snake case:
- Start the file name with a lowercase letter
- Only use alphanumeric characters, lowercase when applicable
- Separate distinct words with an underscore

## Use a Module
Once your module is created, you can write your code
```Python
def greet_person(person):
        print("Hello " + person)

# __name__ is an attribute that helps determine if content from a module should be used or not.
# In this case, the code in the if block will only trigger if this module is executed directly,
# this is because the __name__ attribute of the module executed directly is set to "__main__".
# If a module is not directly executed but still used (through importing), its __name__ is set
# to the name of the module, excluding the .py extension.
if __name__ == "__main__":
 greet_person("Bob")
```
Once your module is set, you can execute it with your interpreter. Depending on what OS you are working with, the specific command will be different, but assuming you are on Windows, you can use the command "py" to target your machine's default version of Python.
```cmd
py my_module.py
Hello Bob
```

## Importing Modules
If you want to make use of your module in a second module, you have to import the data. You can import the function from the module specifically, or you can import the module and call the function from it.

In the examples below, assume the two modules are in the same directory.
```Python
# in a second module

# import the function
from my_module import greet_person

# Call the function directly
greet_person("Sally")
```
```Python
# in a second module

# import the module
import my_module

# Call the function through the module
my_module.greet_person("Sally")
```
```cmd
py my_second_module.py
Hello Sally
```

## Using Aliases with Modules
When importing lots of data, it is common practice to set "aliases" for your imports. Aliases are variables that represent whatever you import, and you set them when you first perform the import.
```Python
from my_module import greet_person as greeting

greeting("Timmy")
```
```cmd
py my_second_module.py
Hello Timmy
```

</details>
<details><summary>Summary</summary>

# Summary 

- Modules are files containing Python code
- Modules are typically named following snake case formatting
- If a module is executed directly, its "__name__" attribute is set to "__main__"; otherwise, it's whatever the module name is minus the file extension
- When importing modules, you can import the entire module or specific data from the module
- When importing data, you can create aliases for the data 

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
