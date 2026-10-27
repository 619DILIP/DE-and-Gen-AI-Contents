<details><summary>Learning Objectives</summary>
<br>

* Understand the List datatype
* Understand how to use common List methods

</details>

<details><summary>Description</summary>
<br>

A List is an ordered and mutable group of values. The order of the values within the list is maintained using numbered positions, or indices. Mutable means that after the creation of a list, we can edit the contents of the list, such as adding or removing values or replacing values. Because lists are sequences, or ordered groups of values, they work similarly to strings. We can use the `len()` function, slice them, and use square brackets to access data, with the first element at index 0.

List literals are a comma-separated list of values within square brackets:
```python
myList = [1, 2, 3, 4, 5]
```

### Characteristics of a list:

* ordered by index
* mutable 
* allows duplicate values
* can contain values of different datatypes
* can contain other lists within it
* supports concatenation and slicing

### List methods:

* `append()` -  Adds an element at the end of the list
* `clear()` -   Removes all the elements from the list
* `copy()` -   Returns a copy of the list
* `count()` -  Returns the number of elements with the specified value
* `extend()` -   Adds the elements of a list (or any iterable) to the end of the current list
* `index()` -   Returns the index of the first element with the specified value
* `insert()` -   Adds an element at the specified position
* `pop()` -   Removes the element at the specified position
* `remove()` -   Removes the item with the specified value
* `reverse()` -   Reverses the order of the list
* `sort()` -   Sorts the list

</details>

<details><summary>Real World Application</summary>

<br>
Here are some real-world use cases for the list data type in Python:

1. **Data Storage**: Lists can be used to store and manipulate various types of data, such as numbers, strings, objects, or even other lists (nested lists). This makes lists suitable for applications that require handling structured data, such as databases, inventory management systems, or data analysis tools.
2. **File Operations**: When working with files, lists can be used to store the contents of a file line by line. This is particularly useful when processing large text files or log files, where you can iterate over the list and perform operations on each line.
3. **Stack and Queue Implementations**: Lists can be used to implement basic data structures like stacks (using `append()` and `pop()` methods) and queues (using `append()` and `pop(0)`). These are fundamental data structures used in various algorithms and applications.
4. **Matrix Representation**: Lists of lists can be used to represent matrices or 2D arrays, which are essential in many scientific and computational applications, such as linear algebra, image processing, and data analysis.
5. **Data Manipulation**: Lists provide a wide range of built-in methods and operations for manipulating data, such as sorting, reversing, concatenating, slicing, and more. These operations make it convenient to work with and transform data stored in lists.

These are just a few examples of how lists can be used in real-world Python applications. The versatility of lists makes them a fundamental data structure in Python programming, and their usage extends across various domains, from simple data storage to complex data manipulation and algorithm implementation.

</details>

<details><summary>Implementation</summary> 

### Creating, Adding, and Removing from a List
```python
# creating a list
my_list = [5, 6, 7]

# adding to a list
my_list.append(3)
print(my_list) # [5, 6, 7, 3]

my_list.insert(0, 18)
print(my_list) # [18, 5, 6, 7, 3]

my_other_list = [1, 2]
my_list.extend(my_other_list)
print(my_list) # [18, 5, 6, 7, 3, 1, 2]

# Removing from a list
my_list.remove(5) 
print(my_list) # [18, 6, 7, 3, 1, 2]

my_list.pop()
print(my_list) # [18, 6, 7, 3, 1]

my_list.clear()
print(my_list) # []
```

### Nested Lists
```python
# Create three lists
list_1 = [1, 2, 3]
list_2 = [4, 5, 6]
list_3 = [7, 8, 9]

# Make a list of lists to form a matrix
matrix = [list_1, list_2, list_3]
print(matrix) # [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# access a sub-list's element
value = matrix[1][2]
print(value) # 6
```
### Indexing, Slicing, and Concatenating Lists

```python
my_list = ['apple', 'banana', 'orange', 4, 5.2]

value = my_list[0]
print(value) # apple

value = my_list[3]
print(value) # 4

value = my_list[-1]
print(value) # 5.2

result = my_list[:-1] 
print(result) # ['apple', 'banana', 'orange', 4]

result = my_list[2:]
print(result) # ['orange', 4, 5.2]

result = my_list + ["guava"]
print(result) # ['apple', 'banana', 'orange', 4, 5.2, 'guava']
```
</details>

<details><summary>Summary</summary> 

<br>

* A List is an ordered and mutable group of values
* There are many list methods that can be used to manipulate lists
* Lists also support concatenation and slicing
* The versatility of lists makes them a fundamental data structure in Python programming

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
