# Implementation 

## Create a Module
To create a module you simply make a new file and make sure to give it the ".py" extension. The common convention when creating modules is to use snake case: 
- start the file name with a lowercase letter
- only use alphanumeric characters, lowercase when applicable
- separate distinct words with an underscore


## Use a Module
Once your module is created you can write your code
```python
def greet_person(person):
        print("Hello " + person)

# __name__ is an attribute that helps determine if content from a module should be used or not.
# In this case, the code in the if block will only trigger if this module is executed directly,
# this is because the __name__ attribute of the module executed directly is set to "__main__".
# if a module is not directly executed but still used (through importing) it's __name__ is set
# to the name of the module excluding the .py extension.
if __name__ == "__main__":
        greet_person("Bob")
```
Once your module is set you can execute it with your interpreter. Depending on what OS you are working with the specific command will be different, but assuming you are on windows you can use the command "py" to target your machine's default version of Python.
```cmd
py my_module.py
Hello Bob
```

## Importing Modules
If you want to make use of your module in a second module you have to import the data. You can import the function from the module specifically, or you can import the module and call the function from the module.

In the examples below assume the two modules are in the same directory.
```python
# in a second module

# import the function
from my_module import greet_person

# call the function directly
greet_person("Sally")
```
```python
# in a second module

# import the module
import my_module

# call the function through the module
my_module.greet_person("Sally")
```
```cmd
py my_second_module.py
Hello Sally
```

## Using Aliases with Modules
When importing lots of data it is a common practice to set "aliases" for your imports. Aliases are variables that represent whatever you import you set when you first perform the import.
```Python
from my_module import greet_person as greeting

greeting("Timmy")
```
```cmd
py my_second_module.py
Hello Timmy
```