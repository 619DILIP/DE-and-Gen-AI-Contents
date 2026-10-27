<details><summary>Implementation</summary> 

### Syntax:

```python
range(stop)
range(start, stop)
range(start, stop, step)

# start: The starting value of the range (optional, default is 0).
# stop: The ending value (exclusive) of the range.
# step: The increment (optional, default is 1).
```

* The `range()` function in Python generates a sequence of numbers based on the provided parameters.
* When only stop is provided, the range starts from 0 and goes up to, but does not include, the stop value.
* If start is provided along with stop, the range starts from start and goes up to, but does not include, the stop value.
* The step parameter specifies the increment between each number in the sequence. If omitted, the default increment is 1.
* range generates a sequence of integers, which is commonly used in loops and list comprehensions for iterating through elements or generating lists of numbers.

## Using the range Function in Python:

### Creating a Range:

#### 1. Create a range with a start, stop, and step:

```python
numbers = range(1, 10, 2)
```

* This code snippet creates a range object named numbers starting from 1, ending before 10, and incrementing by 2. The range includes elements 1, 3, 5, 7, and 9.

#### 2. Create a range with only stop value (implicitly starts from 0 and step is 1):

```python
countdown = range(5)
```

* This code snippet creates a range object named countdown starting from 0, ending before 5, and incrementing by 1 (default step).

* The range includes elements 0, 1, 2, 3, and 4.

### Using Range Objects:

#### 1. Iterating through a range:

```python
numbers = range(1, 10, 2)

for num in numbers:
    print(num)
# Output:
# 1
# 3
# 5
# 7
# 9
```

* A for loop is used to iterate through the elements of the range numbers, printing each element one by one.

#### 2. Checking range membership:

```python
numbers = range(1, 10, 2)

if 3 in numbers:
    print("3 is in the range.")
else:
    print("3 is not in the range.")
# Output:
# 3 is in the range.
```

* The `in` keyword checks if a value (in this case, 3) is present in the range numbers.

#### 3. Length of a range:

```python
numbers = range(1, 10, 2)

length = len(numbers)
print("Length of the range:", length)
# Output:
# Length of the range: 5
```

* The `len()` function calculates and prints the length of the range numbers, which is the number of elements it contains.

#### 4. Range as a list:

```python
numbers = range(1, 10, 2)

num_list = list(numbers)
print("Range as a list:", num_list)
# Output:
# Range as a list: [1, 3, 5, 7, 9]
```

* The `list()` function converts the range numbers into a list, which can be printed and manipulated like a regular list.

</details>