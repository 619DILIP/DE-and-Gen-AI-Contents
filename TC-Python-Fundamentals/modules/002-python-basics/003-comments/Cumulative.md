# Cumulative

<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:

- Know what Python comments are.
- Understand the different types of comments.

</details>
<details><summary>Description</summary>
<br>

As applications grow in size and complexity, it becomes increasingly difficult to keep track of what each part of the code is doing. Variables, imports, and logic can quickly become confusing without clear explanations. To address this, Python provides comments as a way to document the intent and behavior of your code, making it easier for both you and others to understand and maintain.

## Commenting in Python

Python supports single-line comments using the `#` symbol. Any text following this symbol on the same line is treated as a comment and ignored during execution. For longer explanations, Python also allows multi-line comments using triple single quotes (`'''`) or triple double quotes (`"""`). These can be especially helpful when documenting more complex sections or adding context to your code.

</details>
<details><summary>Real World Application</summary>

## Importance of Comments in Collaborative Development

In real-world software projects, especially within larger teams or long-term applications, codebases can become highly complex with numerous interdependent features and modules. While the original developer might understand the entire system, future contributors—such as new team members, testers, or maintainers—often do not have the same level of context.

This is where comments play a crucial role.

By adding meaningful comments throughout the code—explaining what a function does, what a variable holds, why a certain approach was used, or warning about non-obvious behavior—you significantly reduce the learning curve for others. Comments act as a guide, making the onboarding process faster and more efficient.

They also help:
- Prevent misunderstandings or incorrect assumptions about how the code works.
- Speed up debugging and future updates.
- Ensure better team collaboration and continuity in case the original developers leave the project.

In short, writing thoughtful comments is not just a good habit—it's a professional necessity in real-world development environments.

</details>
<details><summary>Implementation</summary> 

## Single Comment
To create a single-line comment, you simply add a `#` symbol to the line. The comment is any content after the symbol, so you can write some code before the comment if you want, but not after.
```python
# This is a comment
name = "Ted"  # This is also a comment; the name variable will still be set
```

## Multi-Line Comment
If you need a comment to span multiple lines, you can wrap it in triple single or double quotes.
```python
'''this is a
multi-line
comment'''

"""
You could also
do your comment
this way
"""
```

</details>
<details><summary>Summary</summary> 
<br>

- Comments are for describing features in your code or leaving other developers notes about the code.
- `#` is used to create single-line comments.
- Triple single or double quotes can be used to create multi-line comments.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
