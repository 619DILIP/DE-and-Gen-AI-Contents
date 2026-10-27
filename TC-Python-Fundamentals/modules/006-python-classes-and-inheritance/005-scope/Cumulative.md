<details><summary>Learning Objectives</summary>

* Understand the concept of scope and its significance when writing code
* Explain the difference between the four scopes

</details>

<details><summary>Description</summary>

Scope is the portion of code from which a variable or named Python object is accessible. There are four scopes:

* local - a code block, such as the body of a function or the suite that follows a conditional statement or loop.
* enclosing - if there is a function or code block within a function, then the inner scope can access the variables available in the enclosing function.
* global - the current module. This is the outermost scope an object can be in.
* built-in - the automatically imported module, builtins.

Whenever a reference to a named object is used, the Python interpreter will look for the object in its immediate scope. If the object cannot be found, it will look in the next largest scope, and so on. If there is a local scope, Python will start looking there, then in an enclosing scope, and then in the global scope, including any named imports. If not found there, it will look within the built-in scope.

Knowing how Python resolves named objects is necessary for preventing logical errors in your code. A variable can have the same name as another variable as long as they are not in the same scope. By understanding scope, you can avoid naming conflicts, unintended data modifications, or difficult-to-understand code.

</details>

<details><summary>Real World Application</summary>

A real-world example that illustrates the importance of scope in Python can be seen in the context of building web applications or any software that involves user sessions or multi-user environments.

Consider a scenario where you have a web application that allows multiple users to log in and perform various actions. Each user session should have its own set of variables and data that are isolated from other user sessions. This is where the concept of scope becomes crucial.

Imagine you have a function that handles user authentication and retrieves user information from a database. Inside this function, you might have a variable called `user_id` that stores the unique identifier of the currently logged-in user. If `user_id` had a global scope, it would be accessible and modifiable from anywhere in the application, which could lead to serious security vulnerabilities and data corruption.

By defining `user_id` as a local variable within the authentication function, its scope is limited to that function only. This way, each time the authentication function is called for a different user, a new instance of `user_id` is created, ensuring that each user session has its own isolated `user_id` value.

</details>

<details><summary>Implementation</summary>

Built-In vs global

Below is an example of using the built-in scope. Because the built-in modules are automatically imported, the `eval()` method from that module is used. The `eval()` method parses and evaluates a Python expression.

`x = eval("2 + 2")`
`print(x)  # 4`

We see that the expression `2 + 2` is parsed from the string, and the resulting value is assigned to the variable `x`. We print out the value, and the output is `4`.

The following two examples demonstrate how global scope is searched before built-in scope.

`def eval(input):`
`    return input`

`x = eval("2 + 2")`
`print(x)  # 2 + 2`

In this example, we define a function named `eval()` that returns the value it takes in as input. We then use the same statements as before, where we call the function and print out its value. Notice that the output is `2 + 2` rather than `4`. The globally scoped `eval()` function was used rather than the built-in function.

`from example import eval`

`x = eval("2 + 2")`
`print(x)  # 2 + 2`

In this example, we import a function, `eval()`, from a module named `example`. Let’s assume that the imported function has the same functionality as the one defined in the previous example, where the function returns the value it takes in as input. Again, we see that the output is `2 + 2` rather than `4`. The globally scoped and imported `eval()` function was used rather than the built-in function.

Local vs Enclosing vs Global

In the example below, we will compare local versus global scope.

`x = 1`

`def myFunc():`
`    print(x)  # 1`

`myFunc()`
`print(x)  # 1`

In this example, we can see one variable with the name `x` that is in the global scope. If we use a print statement to print out the value of `x` within the function, the function’s scope will be checked first for a variable with the name `x` before global scope is checked. Because there is no variable created in the local scope with the name `x`, the Python interpreter then checks the global scope. So in this example, both print statements will print out the value of `1`.

`x = 1`

`def myFunc():`
`    x = 2`
`    print(x)  # 2`

`myFunc()  # call myFunc() so it will execute`
`print(x)  # 1`

In this example, we can see two variables with the name `x`. One is within global scope, and the other is in a scope local to a function. If we use a print statement to print out the value of `x` within the function, the function’s scope will be checked first for a variable with the name `x` before global scope is checked. This time, because there is a variable within the function with the name `x`, the locally scoped variable’s value will be used. So in this example, the print statement within the function prints the value of `2`, and the print statement outside of the function prints the value of `1`.

In this last example, let’s also create an enclosing scope.

`x = 1`

`def myFunc():`
`    x = 2`

`    def myInnerFunc():`
`        x = 3`
`        print(x)  # 3`

`    myInnerFunc()  # call myInnerFunc() so it will execute`
`    print(x)  # 2`

`myFunc()  # call myFunc() so it will execute`
`print(x)  # 1`

In this example, we can see three variables with the name `x`. One is within global scope, another in enclosing scope, and the last in a scope local to the innermost function. If we use a print statement in each scope, we can see that in whichever scope the print statement is in, that is the scope that will be checked first. So in this example, the innermost print statement prints `3`, the print statement within the enclosing function prints the value of `2`, and the print statement outside of the function will print the value of `1`.

</details>

<details><summary>Summary</summary>

* Scope is the portion of code from which a variable or named Python object is accessible.
* There are four scopes: local, enclosing, global, and built-in.
* By understanding scope, you can avoid naming conflicts, prevent bugs, and write code that is easier to understand and maintain.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
