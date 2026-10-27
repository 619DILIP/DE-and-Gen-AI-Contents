### Built-In vs global

Below is an example of using built-in scope. Because the builtins modules is automatically imported, the eval() method from that module is used. The eval() method parses and evaluates a Python expression.

```Python
x = eval("2 + 2")
print(x) # 4
```

We see that the expression `2 + 2` is parsed from the string and the resulting value is assigned to the variable `x`. We the print out the value, and the output is `4`.

<br>

The below two examples demonstrate how global scope is searched before built-in scope. 
```Python
def eval(input):
  return input

x = eval("2 + 2")
print(x) # 2 + 2
```
In this example, we define a function named `eval()` that returns the value it takes in as input. We then use the same statements as before where we call the function and print out its value. Notice that the output is `2 + 2` rather than `4`. The globally scoped `eval()` function was used rather than the built-in function.
<br>

```Python
from example import eval

x = eval("2 + 2")
print(x) # 2 + 2
```
In this example, we import a function the function `eval()` from a module named example. Let’s assume that the imported function has the same functionality as the one defined in the previous example, where the function returns the value it takes in as input. Again, we see that the output is `2 + 2` rather than `4`. The globally scoped and imported `eval()` function was used rather than the built-in function.

<br>

### Local vs Enclosing vs Global



In the below example we will compare local versus global scope.
```Python
x = 1

def myFunc():
  print(x) # 1

myFunc()
print(x) # 1
```

In this example, we can see one variable with the name `x` that is in global scope. If we use a print statement to print out the value of x within the function, the function’s scope will be checked first for a variable with the name `x` before global scope is checked. Because there is no variable created in local scope with the name `x`, the Python interpreter then checks global scope. So in this example, both print statements will print out the value of `1`. 

<br>

```Python
x = 1

def myFunc():
  x = 2
  print(x) # 2

myFunc() # call myFunc() so it will execute
print(x) # 1
```

In this example, we can see two variables with the name `x`. One is within global scope and the other is in a scope local to a function. If we use a print statement to print out the value of `x` within the function, the function’s scope will be checked first for a variable with the name `x` before global scope is checked. This time, because there is a variable within the function with the name `x`, the locally scoped variable’s value will be used. So in this example, the print statement within the function prints the value of `2` and the print statement outside of the function will print the value of `1`.

<br>

In this last example, let’s also create an enclosing scope.
```Python
x = 1

def myFunc():
  x = 2

  def myInnerFunc():
    x = 3
    print(x) # 3

  myInnerFunc() # call myInnerFunc() so it will execute
  print(x) # 2

myFunc() # call myFunc() so it will execute
print(x) # 1
```

In this example, we can see three variables with the name `x`. One is within global scope, another in enclosing scope, and the last in a scope local to the innermost function. If we use a print statement in each scope, we can see that in whichever scope the print statement is in, that is the scope that will be checked first. So in this example, the innermost print statement prints `3`, the print statement within the enclosing function prints the value of `2`, and the print statement outside of the function will print the value of `1`.