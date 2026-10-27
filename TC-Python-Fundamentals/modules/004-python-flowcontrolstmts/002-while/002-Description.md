# Description

A **`while`** loop is used to repeatedly execute a block of code as long as a specified condition is true. This provides a way to perform iterative tasks, such as iterating over elements in a list or processing user input until a certain condition is met.

The syntax of a **`while`** loop is as follows:

    while <expr>:
        <statement(s)>

**`<statement(s)>`** represents the block to be repeatedly executed, often referred to as the body of the loop. This is denoted with indentation, just as in an if-statement.

The controlling expression, **`<expr>`**, typically involves one or more variables that are initialized prior to starting the loop and then modified somewhere in the loop body.

When a while loop is encountered, **`<expr>`** is first evaluated in a Boolean context. If it is true, the loop body is executed. Then **`<expr>`** is checked again, and if still true, the body is executed again. This continues until **`<expr>`** becomes false, at which point program execution proceeds to the first statement beyond the loop body.

Python provides two keywords that terminate a loop iteration prematurely:

- The **`break`** statement immediately terminates a loop entirely. Program execution proceeds to the first statement following the loop body.
- The **`continue`** statement immediately terminates the current loop iteration. Execution jumps to the top of the loop, and the controlling expression is re-evaluated to determine whether the loop will execute again or terminate.

The distinction between **`break`** and **`continue`** is demonstrated in the following diagram:

![Example](Images\image.png)

