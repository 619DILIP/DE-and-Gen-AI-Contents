# Implementation 

## Input
You can prompt users to enter data into your application during runtime using the "input" function
```python
user_input = input()
```
To help the user understand what data to provide, you can provide a prompt as well
```python
user_input = input("Enter your name: ")
```

## Print
To display data in the console, you use the "print" function
```python
print("Hello world!")
```
You can pass multiple objects into the function, and they will be separated by a space by default
```python
print("Hello", "world!")
```
If you want to change the separator between objects, you can set a value called "sep" to your desired separator in the function arguments
```python
print("Hello","world!", sep="-")
```
Finally, the default behavior for the function is to end the line with a new line character, which you can change by setting an "end" value in the argument to your desired end character
```python
print("Hello","world", sep="-", end="!")
```
