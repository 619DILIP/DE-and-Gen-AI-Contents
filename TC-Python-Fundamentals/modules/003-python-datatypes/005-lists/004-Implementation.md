
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

# removing from a list
my_list.remove(5) 
print(my_list) # [18, 6, 7, 3, 1, 2]

my_list.pop()
print(my_list) # [18, 6, 7, 3, 1]

my_list.clear()
print(my_list) # []
```

### Nested Lists
```python
# create three lists
list_1 = [1,2,3]
list_2 = [4,5,6]
list_3 = [7,8,9]

# Make a list of lists to form a matrix
matrix = [list_1, list_2, list_3]
print(matrix) # [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# access a sub-list's element

value = matrix[1][2]
print(value) # 6
````
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
print(result) #['apple', 'banana', 'orange', 4]

result =  my_list[2:]
print(result) # ['orange', 4, 5.2]

result = my_list + ["guava"]
print(result) # ['apple', 'banana', 'orange', 4, 5.2, 'guava']
```