# Description

Conditional statements allow you to make decisions and execute specific blocks of code based on certain conditions. There are three types of conditional statements: **`if`**, **`if-else`**, **`if-elif-else`**, and nested **`if`**.

### If statement: 
The simplest form of a conditional statement is the if statement. It allows you to execute a block of code only if a particular condition is true.

 if condition:
 # code to be executed if the condition is true



### If-else statement: 
An if-else statement allows you to execute one block of code if the condition is true and another block of code if the condition is false.

 if condition:
 # code to be executed if the condition is true

 else:
 # code to be executed if the condition is false



### If-elif-else statement: 
An if-elif-else statement is used when you have multiple conditions to check. It allows you to check each condition one by one and execute the code block associated with the first condition that is true. If none of the conditions are true, the code block under the else statement is executed.

 if condition1:
 # code to be executed if condition1 is true

 elif condition2:
 # code to be executed if condition2 is true

 else:
 # code to be executed if both conditions are false



### Nested if statement: 
A nested if statement is one where an if statement is placed inside another if statement. It allows you to make more complex decisions based on multiple conditions.

 if condition1:
 # code to be executed if condition1 is true

 if condition2:
 # code to be executed if both condition1 and condition2 are true

 else:
 # code to be executed if condition1 is true but condition2 is false

 else:
 # code to be executed if condition1 is false
