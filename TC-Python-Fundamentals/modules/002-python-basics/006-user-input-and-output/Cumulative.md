# Cumulative

<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:

- Output data to the console
- Insert data into their applications during runtime

</details>

<details><summary>Description</summary>
<br>

- Python has a myriad of ways to show off data in your code, the simplest being the `print` function. This is a bit of code that will display whatever data you indicate to the terminal you used to execute your code. This typically will display the data you want to see in a form that is human-readable (showing someone's name that you saved in your code, for instance). Still, some data types will display the memory location (where the data resides in the computer) by default. In these cases, you would need to specify how you want the data to be displayed.

- On the flip side, the `input` function allows you to enter data into your application during runtime as a string. If you need your data to be something other than a string, you will have to transform it in your code.

</details>
<details><summary>Real World Application</summary>
<br>

Many applications will require some form of user input for the application to function correctly. In larger enterprise applications, this will typically be handled through a user-friendly interface, but for a smaller script or a personal app, entering relevant data through the command line via `input` is a convenient and quick way of entering data into your application.

Similarly, most major applications are going to output data in some persistent location and use third-party applications to parse and manage the output of the application. However, if you are prototyping your application or working in your terminal, the `print` function is a fantastic tool for displaying output data from your code.

</details>
<details><summary>Implementation</summary> 

## Input
You can prompt users to enter data into your application during runtime using the `input` function
```python
user_input = input()
```
To help the user understand what data to provide, you can provide a prompt as well
```python
user_input = input("Enter your name: ")
```

## Print
To display data in the console, you use the `print` function
```python
print("Hello world!")
```
You can pass multiple objects into the function, and they will be separated by a space by default
```python
print("Hello", "world!")
```
If you want to change the separator between objects, you can set a value called `sep` to your desired separator in the function arguments
```python
print("Hello","world!", sep="-")
```
Finally, the default behavior for the function is to end the line with a new line character, which you can change by setting an `end` value in the argument to your desired end character
```python
print("Hello","world", sep="-", end="!")
```

</details>
<details><summary>Summary</summary> 

# Summary 

- The `input` function allows users to enter string data into the application at runtime.
- The `print` function allows users to display data in the console during runtime.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
