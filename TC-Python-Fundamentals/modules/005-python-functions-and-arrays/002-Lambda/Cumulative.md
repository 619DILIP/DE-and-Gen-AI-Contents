<details><summary>Learning Objectives</summary>
<br>

Learn to use lambdas in Python for concise, anonymous function definitions, enabling efficient coding for simple operations and functional programming paradigms.
</details>

<details><summary>Description</summary>
<br>

Lambda functions, also known as anonymous functions or lambda expressions, are small, single-line functions that can have any number of arguments but only one expression. 

They are defined using the `lambda` keyword and are commonly used when a small function is required for a short period.

</details>

<details><summary>Real-World Application</summary>

### Lambdas are commonly used in Python for:

#### Functional Programming: 
* In functional programming paradigms, lambdas are used extensively to create concise and readable code.

#### Sorting and Filtering:
* Lambdas are often used as key functions in sorting and filtering operations.

#### Event Handling: 

* In GUI applications or event-driven programming, lambdas are used to define callback functions.

#### Mapping and Reducing:

* Lambdas are used with `map()`, `filter()`, and `reduce()` functions to perform operations on iterable objects.

</details>

<details><summary>Implementation</summary>

### Basic Syntax:

```
lambda arguments: expression
```

* A lambda function is a small anonymous function that can have any number of arguments but only one expression. The expression is evaluated and returned as the result of the function.
  

### Lambda function to add two numbers

```
add = lambda x, y: x + y
print(add(5, 3))  # Output: 8
```
* Here, a lambda function `add` is defined that takes two arguments `x` and `y` and returns their sum.
* It is then called with arguments 5 and 3, resulting in the output 8.

### Using Lambdas with Built-in Functions:

#### a. `map()` function:

```
numbers = [1, 2, 3, 4, 5]
squares = list(map(lambda x: x ** 2, numbers))
print(squares)  # Output: [1, 4, 9, 16, 25]
```
* The `map()` function applies the lambda function (squaring each element) to each item in the `numbers` list, resulting in a list of squared numbers.

#### b. `filter()` function:

```
numbers = [1, 2, 3, 4, 5]
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # Output: [2, 4]
```
* The `filter()` function uses the lambda function to filter out even numbers from the `numbers` list, resulting in a list of even numbers.

### Sorting with Lambdas:

```
students = [
    ("John", 25),
    ("Emily", 30),
    ("Adam", 22)
]
students.sort(key=lambda x: x[1])
print(students)  # Output: [('Adam', 22), ('John', 25), ('Emily', 30)]
```
* The `sort()` method of the `students` list is used with a lambda function as the sorting key. 
* The lambda function extracts the second element (age) from each tuple, so the list is sorted based on the students' ages.

</details>


<details><summary>Summary</summary>
<br>

* Lambdas in Python are anonymous functions defined using the `lambda` keyword.

* They are useful for short, one-time functions where defining a regular function would be overkill.

* Lambdas can have any number of arguments but only one expression.

* They are commonly used with built-in functions like `map()`, `filter()`, and `sorted()`, as well as in GUI programming for defining callback functions.
</details>


<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
