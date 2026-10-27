<br>

A List is an ordered and mutable group of values. The order of the values within the list is maintained using numbered positions, or indexes. Mutable means that after the creation of a list, we can edit the contents of the list, such as adding or removing values or replacing values. Because lists are sequences, or ordered groups of values, they work similarly to strings. We can use the len() function, slice them, and use square brackets to access data, with the first element at index 0.

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

* __append()__ -  Adds an element at the end of the list
* __clear()__ -   Removes all the elements from the list
* __copy()__ -   Returns a copy of the list
* __count()__ -  Returns the number of elements with the specified value
* __extend()__ -   Add the elements of a list (or any iterable), to the end of the current list
* __index()__ -   Returns the index of the first element with the specified value
* __insert()__ -   Adds an element at the specified position
* __pop()__ -   Removes the element at the specified position
* __remove()__ -   Removes the item with the specified value
* __reverse()__ -   Reverses the order of the list
* __sort()__ -   Sorts the list