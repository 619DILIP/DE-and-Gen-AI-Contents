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
* Here, a lambda function `add()` is defined that takes two arguments `x` and `y` and returns their sum.
* It is then called with arguments 5 and 3, resulting in the output 8.

### Using Lambdas with Built-in Functions:

#### a. map() function:

```
numbers = [1, 2, 3, 4, 5]
squares = list(map(lambda x: x ** 2, numbers))
print(squares)  # Output: [1, 4, 9, 16, 25]
```
* The `map()` function applies the lambda function (squaring each element) to each item in the numbers list, resulting in a list of squared numbers.

#### b. filter() function:

```
numbers = [1, 2, 3, 4, 5]
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # Output: [2, 4]
```
* The `filter()` function uses the lambda function to filter out even numbers from the numbers list, resulting in a list of even numbers.

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
* The `sort()` method of the students list is used with a lambda function as the sorting key. 
* The lambda function extracts the second element (age) from each tuple, so the list is sorted based on the students ages.

</details>
