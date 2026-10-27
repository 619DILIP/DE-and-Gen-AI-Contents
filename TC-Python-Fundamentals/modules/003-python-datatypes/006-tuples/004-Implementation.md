
### Packing and Unpacking

Packing is where we can assign a comma-separated list of values to a single variable. This creates a tuple. You can optionally use parenthesis to surround the values. 

Unpacking is where you can assign variables the values within a tuple. In order for unpacking to work, the amount of variables you use must be the same as the amount of values in the data structure.
```python
# packing
my_tuple = 1, 2, 3, 4, 5
print(my_tuple) # (1, 2, 3, 4, 5)

# unpacking
a, b, c, d, e = my_tuple

print(b) # 2
```

We can see that when we assign comma-separated values to a variable, they are “packed up” into a tuple, meaning a tuple is created that contains those values. When we assign multiple variables to a tuple, what we’re doing is assigning each variable the corresponding value in the tuple. The first variable is given the first value in the tuple and so on. When we print the value of b, since it is the second variable being assigned, it receives the second value in the tuple, which is 2. 

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