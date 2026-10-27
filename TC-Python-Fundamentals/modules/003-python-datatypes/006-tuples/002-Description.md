<br>

A Tuple is an ordered and immutable group of values. The order of the values within the list is maintained using numbered positions, or indexes. Immutable means that after the creation of a tuple, we cannot edit its contents. Because tuples are sequences, or ordered groups of values, we can perform operations such as slicing or using the len() function.

Tuple literals are a comma-separated list of values that are commonly enclosed in parenthesis:
```python
my_tuple = (1, 2, 3, 4, 5)
```


Like lists, sets, and dictionaries, tuples can also be created using a function. For tuples the function is tuple():
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
* supports slicing and the use of len()

###  Tuple methods:

* __len()__ - Returns the amount of elements within the tuple 
* __count()__ - Returns the number of elements with the specified value
*  __index()__ - Returns the index of the first element with the specified value