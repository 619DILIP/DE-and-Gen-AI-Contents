# Cumulative

<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:

 - Explain the use of operators
 - Identify common use cases for using operators

</details>

<details><summary>Description</summary>
<br>

In Python programming, a key aspect is enabling different resources—such as numbers, strings, or data structures—to interact with one another. These interactions are commonly handled using operators, which are built-in symbols or keywords that define specific behaviors between data types.

For example, using the `+` operator on two numbers results in their sum, while using it on two strings concatenates them. Python provides a wide range of operators that support arithmetic, comparison, logical evaluation, and more. Each built-in data type comes with its default behavior for these operators.

Additionally, Python allows developers to define custom behavior for these operators when working with user-defined types, offering flexibility in how objects interact. This operator functionality is essential for creating expressive, readable, and efficient code in real-world applications.

</details>
<details><summary>Real World Application</summary>
<br>

Unless you are writing the most basic of scripts, you will likely need to make use of one or more operators in your code. Operators are a fundamental component of writing code; you will need them far more often than not.

The good news about this is that their use will become second nature to you, since most of the time you will only need their default functionality.

</details>
<details><summary>Implementation</summary> 
<br>

To use operators, you simply place them between the values you want to interact with. Depending on the data types involved, you will get different results. For instance, if you use an addition operator on two integers, you will get their sum. However, if you use the addition operator on two strings, you will get string concatenation (a single string that is the combination of the two strings will be created). Some of these operators may not make much sense until you get to their use cases in later modules.

## Arithmetic Operators
```python
+  # addition
-  # subtraction
*  # multiplication
/  # division
** # power of
%  # modulus
// # floor division
```

## Assignment Operators
```python
=  # assigns a value to a variable
+= # adds to the existing variable's value
-= # subtracts from the existing variable's value
*= # multiplies the existing variable's value by a value
/= # divides the existing variable's value by a value
%= # returns the modulus of the existing variable value
//= # returns floor division with the existing variable value
**= # raises the existing variable's value to a power
```

## Comparison Operators
```python
!= # checks if values are not equal
== # checks if values are equal
>  # checks if the first value is greater than the second
<  # checks if the first value is less than the second
>= # checks if the first value is greater than or equal to the second
<= # checks if the first value is less than or equal to the second
```

## Logical Operators
```python
is       # checks if objects share a memory address
is not   # checks if objects do not share a memory address
and      # requires multiple logical checks to be true to continue code execution
or       # specifies multiple logical checks where only one needs to be true to continue code execution
```

## Membership Operators
```python
in      # returns True if the object is in a collection
not in  # returns True if the object is not in a collection
```

</details>
<details><summary>Summary</summary>  

# Summary 

- Operators allow for performing various actions on data in your code.
- Operators have default behaviors for different data types.
- Python supports configuring how operators work on some of your custom data.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
