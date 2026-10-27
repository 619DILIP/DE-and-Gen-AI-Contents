<details><summary>Learning Objective</summary>
<br>
Master the use of iterators in Python to efficiently traverse and process elements in data structures such as lists, tuples, and dictionaries, enhancing code readability and performance.
</details>

<details><summary>Description</summary>
<br>

* Iterators are objects in Python that allow looping through a sequence of elements, such as lists, tuples, or dictionaries.

* They provide a way to access elements one by one without needing to know the underlying data structure.

</details>
<details><summary>Real-World Application</summary>

### Iterators in Python are commonly used for:

#### Efficient Iteration:
* Looping through large datasets without loading them entirely into memory.

#### Lazy Evaluation:
* Processing elements only when needed, which improves performance.

#### Custom Iterators:
* Creating custom classes that support iteration for specialized data structures.

#### Streaming Data: 
* Handling streams of data from external sources or files.

</details>

<details><summary>Implementation</summary>

### Creating an Iterator:

#### a. Using a for loop:

```py
numbers = [1, 2, 3, 4, 5]
for num in numbers:
    print(num)
```

* The for loop iterates over each element in the numbers list and prints it. 
* This is a straightforward way to iterate over iterable objects like lists.


#### b. Using `iter()` and `next()`:

```py
numbers = [1, 2, 3, 4, 5]
iter_numbers = iter(numbers)
print(next(iter_numbers))  # Output: 1
print(next(iter_numbers))  # Output: 2
```

* The `iter()` function creates an iterator object from the numbers list. 
* The `next()` function is used to retrieve elements from the iterator sequentially.
* After each call to `next()`, the iterator advances to the next element.

### Custom Iterator Class:

```py
class MyIterator:
    def __init__(self, data):
        self.data = data
        self.index = 0
    def __iter__(self):
        return self
    def __next__(self):
        if self.index >= len(self.data):
            raise StopIteration
        value = self.data[self.index]
        self.index += 1
        return value

numbers = [1, 2, 3, 4, 5]
my_iter = MyIterator(numbers)
for num in my_iter:
    print(num)

```

* This code defines a custom iterator class `MyIterator` that iterates over elements in the data list provided during initialization. 
* The `__iter__()` method returns the iterator object itself, and the `__next__()` method defines the logic for iterating through elements. 
* The for loop then uses this custom iterator to iterate over numbers.

### Using Iterators with Generators:
```py
def square_numbers(nums):
    for num in nums:
        yield num * num

numbers = [1, 2, 3, 4, 5]
squares = square_numbers(numbers)
for square in squares:
    print(square)
```

* The `square_numbers()` function is a generator that yields the square of each number in `nums`. 
* When `square_numbers(numbers)` is called, it returns a generator object.
* The for loop iterates over the generator, lazily computing and printing squared values as needed.

### Built-in Iterators:

#### a. `range()` function:
```py
for i in range(5):
    print(i)
```

* The `range()` function generates a sequence of numbers from 0 to 4 (5 elements) and provides an iterator. 
* The for loop then iterates over this iterator, printing each number in the sequence.

#### b. `enumerate()` function:
```py
fruits = ['apple', 'banana', 'cherry']
for index, fruit in enumerate(fruits):
    print(index, fruit)
```

* The `enumerate()` function returns an iterator that yields tuples containing an index and the corresponding element from `fruits`. 
* The for loop iterates over this iterator, unpacking each tuple into index and fruit variables and printing them.
</details>

<details><summary>Summary</summary>
<br>

* Iterators in Python allow for efficient and lazy evaluation of elements in a sequence.

* They can be created using built-in functions like `iter()` and `next()`, as well as by defining custom iterator classes.

* Custom iterators provide flexibility and can be used with any data structure.

* Generators are a special type of iterator that simplifies the creation of iterators using the `yield` keyword.

* Built-in iterators like `range()` and `enumerate()` are commonly used for looping through sequences and obtaining indices along with values.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
