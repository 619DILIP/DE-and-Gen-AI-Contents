# Implementation 

Here are some examples of implementing conditional statements:

### If statement:

        age = 18

        if age >= 18:
                print("You are an adult.")

In the above code example, a variable **`age`** is assigned the value 18. The subsequent **`if`** statement checks if the value of **`age`** is greater than or equal to 18. If this condition is true, the indented block of code following the **`if`** statement is executed, which in this case is the **`print`** statement.

So, when the code is running and **`age`** is 18 or greater, the output will be "You are an adult." Otherwise, if **`age`** is less than 18, no output will be generated because the condition is not met.


### If-else statement:

        age = 16

        if age >= 18:
                print("You are an adult.")

        else:
                print("You are a minor.")

In the above code example, a variable **`age`** is assigned the value 16. The subsequent **`if`** statement checks if the value of **`age`** is greater than or equal to 18. If this condition is true, the indented block of code following the **`if`** statement is executed, which would be the first **`print`** statement. However, since the condition is not met (16 is not greater than or equal to 18), the code moves to the **`else`** block.

The **`else`** block is executed when the condition in the **`if`** statement is false. In this case, it contains the **`print`** statement that outputs "You are a minor."

Therefore, when the code is running with **`age`** being 16, the output will be "You are a minor." This is because the **`else`** block is triggered when the condition in the **`if`** statement is not satisfied.


### If-elif-else statement:

        score = 85

        if score >= 90:
                print("You scored an A grade.")

        elif score >= 80:
                print("You scored a B grade.")

        else:
                print("You scored a C grade.")

In the above code example,

1. The variable **`score`** is assigned the value 85.
2. The first **`if`** statement checks if the value of **`score`** is greater than or equal to 90. If this condition is true, the code inside the block is executed, which would output "You scored an A grade."
3. If the condition in the first **`if`** statement is false, the **`elif`** (else if) statement is evaluated. In this case, it checks if the score is greater than or equal to 80. If this condition is true, the corresponding block of code is executed, which outputs "You scored a B grade."
4. If both the **`if`** and **`elif`** conditions are false, the code inside the **`else`** block is executed, which would output "You scored a C grade."

Given that **`score`** is 85, the condition in the first **`if`** statement is false, but the condition in the **`elif`** statement is true. Therefore, the output of the code will be "You scored a B grade."


### Nested if statement:

        age = 18
        
        grade = "B"

        if age >= 18:

                if grade == "A":
                        print("You are an adult with an A grade.")

                else:
                        print("You are an adult with a grade other than A.")

        else:
                print("You are a minor.")

In the above code example,

1. The variable **`age`** is assigned the value 18, and **`grade`** is assigned the value "B".
2. The first **`if`** statement checks if the value of **`age`** is greater than or equal to 18. If this condition is true, the code inside the block is executed.
3. Inside the first **`if`** block, there's another **`if`** statement that checks if the value of **`grade`** is "A". If this condition is true, the code inside this nested **`if`** block is executed, which outputs "You are an adult with an A grade."
4. If the condition in the nested **`if`** statement is false, the **`else`** block of the nested **`if`** statement is executed, which outputs "You are an adult with a grade other than A."
5. If the condition in the first **`if`** statement is false, the code inside the **`else`** block of the first **`if`** statement is executed, which would output "You are a minor."

Given that **`age`** is 18 and **`grade`** is "B", the condition in the first **`if`** statement is true. Then, since the condition in the nested **`if`** statement is false, the output of the code will be "You are an adult with a grade other than A."

