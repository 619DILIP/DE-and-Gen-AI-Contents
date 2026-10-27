<details><summary>Learning Objectives</summary>
<br>

* Understand the Tuple datatype

</details>

<details><summary>Description</summary>
<br>

A Tuple is an ordered and immutable group of values. The order of the values within the tuple is maintained using numbered positions, or indices. Immutable means that after the creation of a tuple, we cannot edit its contents. Because tuples are sequences, or ordered groups of values, we can perform operations such as slicing or using the `len()` function.

Tuple literals are a comma-separated list of values that are commonly enclosed in parentheses:
```python
my_tuple = (1, 2, 3, 4, 5)
```

Like lists, sets, and dictionaries, tuples can also be created using a function. For tuples, the function is `tuple()`:
```python
original = 1, 2, 3, 4, 5
copy = tuple(original)
```

### Characteristics of a tuple:

* ordered by index
* immutable
* can be nested
* can contain values of different datatypes
* can contain mutable objects, such as lists
* supports slicing and the use of `len()`

### Tuple methods:

* `len()` - Returns the number of elements within the tuple 
* `count()` - Returns the number of elements with the specified value
* `index()` - Returns the index of the first element with the specified value

</details>

<details><summary>Real World Application</summary>
<br>
Although tuples may seem more restrictive than lists, they have several practical use cases in real-world Python applications:

1. **Constant Data**: Tuples are commonly used to store data that should remain constant throughout the program's execution, such as configuration values, user preferences, or fixed parameters. Their immutability ensures that the data cannot be accidentally modified, providing a layer of safety.
2. **Heterogeneous Data Storage**: Tuples can store elements of different data types, making them suitable for storing heterogeneous data structures. For example, you might use a tuple to represent a record with fields like name (string), age (integer), and grade (float).
3. **Database Operations**: When working with databases, tuples are often used to represent rows or records fetched from a database query. The immutability of tuples ensures that the data remains consistent and cannot be accidentally altered.
4. **Keys in Dictionaries**: Tuples, being immutable, can be used as keys in dictionaries, whereas lists cannot because they are mutable. This property makes tuples useful for creating dictionaries with complex keys, such as pairs or triplets of values.
5. **Data Integrity**: Because tuples are immutable, they can be used to ensure data integrity in applications where data should not be modified after initial processing or validation. This can be useful in scientific computing, financial applications, or any scenario where data tampering must be prevented.

In summary, tuples are useful when you need an ordered collection of items that should remain constant. Their immutability and ability to store heterogeneous data make them a valuable data structure in Python programming, particularly in scenarios where data integrity and consistency are crucial.

</details>

<details><summary>Implementation</summary> 

### Packing and Unpacking

Packing is where we can assign a comma-separated list of values to a single variable. This creates a tuple. You can optionally use parentheses to surround the values.

Unpacking is where you can assign variables the values within a tuple. In order for unpacking to work, the number of variables you use must be the same as the number of values in the data structure.
```python
# packing
my_tuple = 1, 2, 3, 4, 5
print(my_tuple) # (1, 2, 3, 4, 5)

# unpacking
a, b, c, d, e = my_tuple

print(b) # 2
```

We can see that when we assign comma-separated values to a variable, they are “packed up” into a tuple, meaning a tuple is created that contains those values. When we assign multiple variables to a tuple, what we’re doing is assigning each variable the corresponding value in the tuple. The first variable is given the first value in the tuple, and so on. When we print the value of `b`, since it is the second variable being assigned, it receives the second value in the tuple, which is `2.`

### Common Tuple Operations
```python
my_tuple = 1, 1, 2, 4, 3, 3, 1
print(my_tuple) # (1, 1, 2, 4, 3, 3, 1)

# accessing indexes
print(my_tuple[1]) # 1
print(my_tuple.index(4)) # 3

# counting occurrences
print(my_tuple.count(3)) # 2

# slicing
print(my_tuple[:2]) # (1, 1)
print(my_tuple[:-2]) # (1, 1, 2, 4, 3)
```

</details>

<details><summary>Summary</summary> 

<br>

* A Tuple is an ordered and immutable group of values. 
* They are frequently used to pack/unpack values.
* Common operations to perform on a tuple are using `index()`, `count()`, or the `len()` function.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
