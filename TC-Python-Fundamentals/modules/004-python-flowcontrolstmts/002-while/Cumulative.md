# While Loop
<details><summary>Learning Objectives</summary>
<br>

After completing this module, you should be able to:

- Understand the concept of a while loop in Python and its syntax.
- Learn how to use while loops to repeatedly execute a block of code as long as a specified condition is true.
- Recognize scenarios where while loops are appropriate for solving problems.
- Understand how to avoid infinite loops and ensure proper termination conditions.
- Gain proficiency in implementing while loops effectively in Python programs.

</details>
<details><summary>Description</summary>

# Introduction

A **`while`** loop is used to repeatedly execute a block of code as long as a specified condition is true. This provides a way to perform iterative tasks, such as iterating over elements in a list or processing user input until a certain condition is met.

The syntax of a **`while`** loop is as follows:

    while <expr>:
        <statement(s)>

**`<statement(s)>`** represents the block to be repeatedly executed, often referred to as the body of the loop. This is denoted with indentation, just as in an if-statement.

The controlling expression, **`<expr>`**, typically involves one or more variables that are initialized prior to starting the loop and then modified somewhere in the loop body.

When a while loop is encountered, **`<expr>`** is first evaluated in a Boolean context. If it is true, the loop body is executed. Then **`<expr>`** is checked again, and if it is still true, the body is executed again. This continues until **`<expr>`** becomes false, at which point program execution proceeds to the first statement beyond the loop body.

Python provides two keywords that terminate a loop iteration prematurely:

- The **`break`** statement immediately terminates a loop entirely. Program execution proceeds to the first statement following the loop body.
- The **`continue`** statement immediately terminates the current loop iteration. Execution jumps to the top of the loop, and the controlling expression is re-evaluated to determine whether the loop will execute again or terminate.

The distinction between **`break`** and **`continue`** is demonstrated in the following diagram:

![Example](Images/image.png)

</details>
<details><summary>Real World Application</summary>
<br>
While loops are commonly used in various real-world applications, such as:

* User Input Validation: Continuously prompting the user for input until valid data is provided.
* Data Processing: Iterating over large datasets to perform computations or analysis.
* Simulation and Modeling: Implementing iterative algorithms and simulations for scientific or engineering applications.
* Interactive Programs: Creating interactive interfaces that respond to user input in real-time.
* Game Development: While loops are commonly used to handle game loops, where the game continues to run until a specific condition is met (e.g., the player quits or the game is over).
* File Processing: While loops can be used to read or write data from/to files until the end of the file is reached.
* Network Programming: While loops are employed in network applications to continuously listen for incoming connections or data until a specific event occurs (e.g., a client disconnects).

</details>
<details><summary>Implementation</summary> 
<br>

Here are some examples of implementing a while loop:

    n = 5

    while n > 0:       
        n -= 1
        print(n)

Here’s what’s happening in this example:

* **`n`** is initially **`5`**. The expression in the **`while`** statement header on line 2 is **`n > 0`**, which is true, so the loop body executes. Inside the loop body on line 3, **`n`** is decremented by **`1`** to **`4`**, and then printed.
* When the body of the loop has finished, program execution returns to the top of the loop at line 2, and the expression is evaluated again. It is still true, so the body executes again, and **`3`** is printed.
* This continues until **`n`** becomes **`0`**. At that point, when the expression is tested, it is false, and the loop terminates. Execution would resume at the first statement following the loop body, but there isn’t one in this case.

Note that the controlling expression of the **`while`** loop is tested first, before anything else happens. If it’s false to start with, the loop body will never be executed at all.

In the example above, when the loop is encountered, **`n`** is **`0`**. The controlling expression **`n > 0`** is already false, so the loop body never executes.

Here’s another **`while`** loop involving a break statement:

    n = 5

    while n > 0:
        n -= 1

        if n == 2:
            break

        print(n)

    print('Loop ended.')

When **`n`** becomes **`2`**, the **`break`** statement is executed. The loop is terminated completely, and program execution jumps to the print() statement on line 7.

Here’s another **`while`** loop involving a continue statement:

    n = 5

    while n > 0:
        n -= 1

        if n == 2:
            continue

        print(n)

    print('Loop ended.')

This time, when **`n`** is **`2`**, the **`continue`** statement causes termination of that iteration. Thus, **`2`** isn’t printed. Execution returns to the top of the loop, the condition is re-evaluated, and it is still true. The loop resumes, terminating when **`n`** becomes **`0`**, as previously.

</details>
<details><summary>Summary</summary> 
<br>

* The **`while`** loop repeatedly executes a block of code as long as the specified condition is true.
* The condition is evaluated before each iteration of the loop.
* If the condition is initially false, the loop body is never executed.
* It's crucial to ensure that the condition eventually becomes false to prevent an infinite loop.
* The **`break`** statement can be used to exit the loop prematurely, and the **`continue`** statement can be used to skip the current iteration and move to the next one.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
