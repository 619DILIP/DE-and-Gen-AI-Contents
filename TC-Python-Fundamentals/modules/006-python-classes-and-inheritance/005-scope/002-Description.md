Scope is the portion of code that a variable or named Python object is accessible from. There are four scopes:

* **local** - a code block, such as the body of a function or the suite that follows a conditional statement or loop. 
* **enclosing** - if there is a function or code block within a function, then the inner scope can access the variables available in the enclosing function.
* **global** - the current module. This is the outermost scope an object can be in. 
* **built-in** - the automatically imported module, builtins. 

Whenever a reference to a named object is used, the Python interpreter will look for the object in its immediate scope. If the object cannot be found, then it will look in the next largest scope, and so on. If there is a local scope, Python will start looking there, then in an enclosing scope, then it will look in global scope, including in any named imports. If not found there, it will look within the built-in scope.


Knowing how Python resolves finding named objects is necessary for preventing logical errors in your code. A variable can have the same name as another variable as long as they are not in the same scope. By understanding scope, you can avoid naming conflicts, unintended data modifications, or difficult to understand code.