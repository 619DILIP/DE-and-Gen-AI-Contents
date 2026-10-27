# Cumulative for the if else
<details><summary>Learning Objectives</summary>
<br>

After completing this module, you should be able to:

- Understand the syntax and structure of **`if`**, **`if-else`**, **`if-elif-else`**, and nested **`if`** statements in Python.
- Learn how to use conditional statements for making decisions in code.
- Understand the concept of conditional execution and control flow.
- Learn how to implement **`if`**, **`if-else`**, **`if-elif-else`**, and nested **`if`** statements in Python programs.
- Understand how to use conditional statements in real-world applications.

</details>
<details><summary>Description</summary>
<br>

Conditional statements allow you to make decisions and execute specific blocks of code based on certain conditions. There are three types of conditional statements: **`if`**, **`if-else`**, **`if-elif-else`**, and nested **`if`**.

### If statement: 
The simplest form of a conditional statement is the **`if`** statement. It allows you to execute a block of code only if a particular condition is true.

```python
if condition:
    # code to be executed if the condition is true
```

### If-else statement: 
An **`if-else`** statement allows you to execute one block of code if the condition is true and another block of code if the condition is false.

```python
if condition:
    # code to be executed if the condition is true
else:
    # code to be executed if the condition is false
```

### If-elif-else statement: 
An **`if-elif-else`** statement is used when you have multiple conditions to check. It allows you to check each condition one by one and execute the code block associated with the first condition that is true. If none of the conditions are true, the code block under the **`else`** statement is executed.

```python
if condition1:
    # code to be executed if condition1 is true
elif condition2:
    # code to be executed if condition2 is true
else:
    # code to be executed if both conditions are false
```

### Nested if statement: 
A nested **`if`** statement is one where an **`if`** statement is placed inside another **`if`** statement. It allows you to make more complex decisions based on multiple conditions.

```python
if condition1:
    # code to be executed if condition1 is true
    if condition2:
        # code to be executed if both condition1 and condition2 are true
    else:
        # code to be executed if condition1 is true but condition2 is false
else:
    # code to be executed if condition1 is false
```

</details>
<details><summary>Real World Application</summary>
<br>

Conditional statements are used in many real-world applications where decisions need to be made based on certain conditions. Some examples include:

- **Traffic lights:** Conditional statements are used to control traffic lights based on traffic volume and signal timings.
- **Automated systems:** Conditional statements are used in automated systems to make decisions based on sensor data and user inputs.
- **Game development:** Conditional statements are used in game development to implement different game rules and logic based on player actions.
- **Weather forecasting:** Making decisions based on temperature, humidity, and other weather conditions.
- **Financial applications:** Processing transactions, applying business rules, and determining eligibility for financial products.
- **User authentication:** Implementing logic to validate user credentials before granting access.

</details>
<details><summary>Implementation</summary> 
<br>

Here are some examples of implementing conditional statements:

### If statement:

```python
age = 18

if age >= 18:
    print("You are an adult.")
```

In the above code example, a variable **`age`** is assigned the value 18. The subsequent **`if`** statement checks if the value of **`age`** is greater than or equal to 18. If this condition is true, the indented block of code following the **`if`** statement is executed, which in this case is the **`print`** statement.

So, when the code is running and **`age`** is 18 or greater, the output will be "You are an adult." Otherwise, if **`age`** is less than 18, no output will be generated because the condition is not met.

### If-else statement:

```python
age = 16

if age >= 18:
    print("You are an adult.")
else:
    print("You are a minor.")
```

In the above code example, a variable **`age`** is assigned the value 16. The subsequent **`if`** statement checks if the value of **`age`** is greater than or equal to 18. If this condition is true, the indented block of code following the **`if`** statement is executed, which would be the first **`print`** statement. However, since the condition is not met (16 is not greater than or equal to 18), the code moves to the **`else`** block.

The **`else`** block is executed when the condition in the **`if`** statement is false. In this case, it contains the **`print`** statement that outputs "You are a minor."

Therefore, when the code is running with **`age`** being 16, the output will be "You are a minor." This is because the **`else`** block is triggered when the condition in the **`if`** statement is not satisfied.

### If-elif-else statement:

```python
score = 85

if score >= 90:
    print("You scored an A grade.")
elif score >= 80:
    print("You scored a B grade.")
else:
    print("You scored a C grade.")
```

In the above code example,

1. The variable **`score`** is assigned the value 85.
2. The first **`if`** statement checks if the value of **`score`** is greater than or equal to 90. If this condition is true, the code inside the block is executed, which would output "You scored an A grade."
3. If the condition in the first **`if`** statement is false, the **`elif`** (else if) statement is evaluated. In this case, it checks if the score is greater than or equal to 80. If this condition is true, the corresponding block of code is executed, which outputs "You scored a B grade."
4. If both the **`if`** and **`elif`** conditions are false, the code inside the **`else`** block is executed, which would output "You scored a C grade."

Given that **`score`** is 85, the condition in the first **`if`** statement is false, but the condition in the **`elif`** statement is true. Therefore, the output of the code will be "You scored a B grade."

### Nested if statement:

```python
age = 18
grade = "B"

if age >= 18:
    if grade == "A":
        print("You are an adult with an A grade.")
    else:
        print("You are an adult with a grade other than A.")
else:
    print("You are a minor.")
```

In the above code example,

1. The variable **`age`** is assigned the value 18, and **`grade`** is assigned the value "B".
2. The first **`if`** statement checks if the value of **`age`** is greater than or equal to 18. If this condition is true, the code inside the block is executed.
3. Inside the first **`if`** block, there's another **`if`** statement that checks if the value of **`grade`** is "A". If this condition is true, the code inside this nested **`if`** block is executed, which outputs "You are an adult with an A grade."
4. If the condition in the nested **`if`** statement is false, the **`else`** block of the nested **`if`** statement is executed, which outputs "You are an adult with a grade other than A."
5. If the condition in the first **`if`** statement is false, the code inside the **`else`** block of the first **`if`** statement is executed, which would output "You are a minor."

Given that **`age`** is 18 and **`grade`** is "B", the condition in the first **`if`** statement is true. Then, since the condition in the nested **`if`** statement is false, the output of the code will be "You are an adult with a grade other than A."

</details>
<details><summary>Summary</summary> 
<br>

Conditional statements are essential for making decisions and controlling the flow of a program based on different conditions. The **`if`**, **`if-else`**, **`if-elif-else`**, and nested **`if`** statements allow you to execute specific blocks of code based on the evaluation of conditions. By using these conditional statements effectively, you can create more complex and dynamic programs.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
