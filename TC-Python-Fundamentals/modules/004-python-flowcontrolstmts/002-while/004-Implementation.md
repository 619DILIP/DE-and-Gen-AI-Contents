# Implementation 

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
