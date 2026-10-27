# Cumulative

<details><summary>Learning Objectives</summary>
<br>

After completing this module, you should be able to:

* Understand the concept and purpose of the for loop.
* Learn the syntax and structure of the for loop.
* Iterate over different data structures like lists, tuples, strings, and dictionaries.
* Explore real-world applications of for loops.
* Recognize scenarios where for loops are beneficial for solving problems efficiently.

</details>
<details><summary>Description</summary>

# Introduction 

The for loop in Python is an iterating function. If you have a sequence object, like a list, you can use the for loop to iterate over the items contained within the list.

The functionality of the for loop isn’t very different from what you see in multiple other programming languages.

### When to use a for loop:

Anytime you need to repeat a block of code a fixed number of times. If you do not know the number of times it must be repeated, use a **`while`** loop statement instead.

The syntax of a **`for`** loop is as follows:

        for <var> in <iterable>:
                <statement(s)>

**`<iterable>`** is a collection of objects—for example, a list or tuple. The **`<statement(s)>`** in the loop body are denoted by indentation, as with all Python control structures, and are executed once for each item in **`<iterable>`**. The loop variable **`<var>`** takes on the value of the next element in **`<iterable>`** each time through the loop.

But what exactly is an iterable? Before examining **`for`** loops further, it will be beneficial to delve deeper into what iterables are in Python.

## Iterables:

The term "iterable" refers to an object that can be used in an iteration process. It is used in two ways:

1. *As an Adjective:* An object can be described as "iterable" if it is capable of being iterated over. For example, a list is an iterable object because you can iterate over its elements using a loop.
2. *As a Noun:* An object can be characterized as "an iterable" if it possesses the ability to be iterated over. In this context, "iterable" is used as a noun to refer to the object itself.

If an object is iterable, it can be passed to the built-in Python function **`iter()`**, which returns an iterator. An iterator is a separate object that is responsible for keeping track of the iteration state and providing a way to access the elements of the iterable one by one.

To illustrate this concept, let's consider the following example:

        mylist = [1, 2, 3, 4, 5]
        mystring = "hello"
        mytuple = (10, 20, 30)

In this example, **`mylist`**, **`mystring`**, and **`mytuple`** are all iterable objects. When you pass them to the **`iter()`** function, it returns an iterator object that can be used to iterate over their elements. For instance:

        list_iter = iter(mylist)
        string_iter = iter(mystring)
        tuple_iter = iter(mytuple)

Now, **`list_iter`**, **`string_iter`**, and **`tuple_iter`** are iterator objects that can be used to access the elements of their respective iterables one by one.

While the terminology might seem repetitive at first, it's essential to understand the distinction between iterables and iterators. Iterables are objects that can be iterated over, while iterators are specialized objects that facilitate the iteration process by keeping track of the current state and providing a way to access the next element.

## Iterators:

After understanding what it means for an object to be iterable and how to obtain an iterator from it using the **`iter()`** function, let's explore what you can do with an iterator.

An iterator is a specialized object that acts as a value producer. It is designed to yield successive values from its associated iterable object, one by one. The iterator keeps track of the current position within the iterable, allowing you to access its elements in a sequential manner.

To retrieve the next value from an iterator, you can use the built-in **`next()`** function. This function takes an iterator as an argument and returns the next value in the sequence. If there are no more values to retrieve, it raises the **`StopIteration`** exception, signaling the end of the iteration.

Here's an example to illustrate the concept:

        mylist = [1, 2, 3, 4, 5]
        list_iter = iter(mylist)

        # Retrieve values from the iterator
        print(next(list_iter))  # Output: 1
        print(next(list_iter))  # Output: 2
        print(next(list_iter))  # Output: 3

        # Continue retrieving values until StopIteration is raised
        while True:
                try:
                        value = next(list_iter)
                        print(value)
                except StopIteration:
                        break

In this example, we first create an iterator **`list_iter`** from the list **`mylist`**. We then use the **`next()`** function to retrieve values from the iterator one by one. The first three calls to **`next(list_iter)`** yield the values **`1`**, **`2`**, and **`3`**, respectively.

After that, we enter a while loop where we continue to call **`next(list_iter)`** until the **`StopIteration`** exception is raised, indicating that there are no more values to retrieve. This approach allows us to iterate over the entire sequence until we've exhausted all the values.

Iterators are powerful because they abstract away the details of how an iterable object stores its values, providing a consistent and straightforward way to access those values one by one. This mechanism is used extensively in Python, especially in looping constructs like for loops and comprehensions, which internally utilize iterators to iterate over iterables.

### The Guts of the Python for Loop

You have now been introduced to all the concepts you need to fully understand how Python’s for loop works. Before proceeding, let’s review the relevant terms:

* **`Iteration:`**      The process of looping through the objects or items in a collection.
* **`Iterable:`**       An object (or the adjective used to describe an object) that can be iterated over.
* **`Iterator:`**       The object that produces successive items or values from its associated iterable.
* **`iter():`**         The built-in function used to obtain an iterator from an iterable.

Now, consider again the simple **`for`** loop example with the help of the syntax mentioned above:

        a = ['foo', 'bar', 'baz']
        for i in a:
                print(i)

The **`for`** loop in Python can be understood entirely in terms of the concepts of iterables and iterators. When you use a **`for`** loop to iterate over an iterable object, such as a list or a string, Python follows a specific sequence of steps behind the scenes.

1. Python calls the **`iter()`** function on the iterable object (**`a`** in this case) to obtain an iterator.
2. Python repeatedly calls the **`next()`** function on the iterator to retrieve each item from the iterable, one by one.
3. The loop body is executed once for each item returned by **`next()`**, with the loop variable (**`i`** in this case) being assigned the current item's value.
4. The loop terminates when the **`next()`** function raises the **`StopIteration`** exception, indicating that there are no more items to retrieve from the iterator.

This sequence of events can be summarized in the following diagram:

![Example](Images\For4.png)

Although this process may seem like "unnecessary monkey business" at first glance, it provides a substantial benefit: Python treats looping over all iterables in exactly the same way, using a consistent and elegant approach.

In Python, iterables and iterators are prevalent:

* Many built-in and library objects are iterable, allowing you to loop over their elements.
* The **`itertools`** module in the Python Standard Library contains numerous functions that return iterables, providing powerful tools for working with sequences.
* User-defined objects created with Python's object-oriented capabilities can be made iterable, allowing you to create custom iterable objects.
* Python also features a construct called a generator, which allows you to create your own iterator in a simple and straightforward way.

Throughout your Python journey, you will discover more about all these concepts. Regardless of the type of iterable you're working with, the for loop syntax remains the same, making it a versatile and elegant construct for iterating over various data structures and sequences.

</details>
<details><summary>Real World Application</summary>
<br>
For loops are commonly applied in real-world scenarios, including:

* **`Data Processing:`** Iterating over elements in a dataset for analysis or computation.
* **`User Interface Handling:`** Managing and processing user interface elements in graphical applications.
* **`Text Processing:`** Analyzing and manipulating text data, such as parsing paragraphs or sentences.
* **`Automated Testing:`** Implementing test cases to iterate over different inputs and expected outputs.
* **`Data Visualization:`** Generating visualizations by iterating over data points and creating plots or charts.
* **`Game Development:`** Iterating over game objects, handling user input, or updating game states.

</details>
<details><summary>Implementation</summary> 
<br>

### 1. Using the for loop to iterate over a Python list or tuple:

Lists and tuples are sequences in Python, making them perfect for iteration using **`for`** loops. Here's an example:

        fruits = ["apple", "banana", "cherry"]

        for fruit in fruits:
                print(fruit)

        # Output:
        # apple
        # banana
        # cherry

In this example, the **`for`** loop iterates over each element in the **`fruits`** list, and the loop variable **`fruit`** takes on the value of each element during each iteration.

### 2. Nesting Python for loops:

You can nest **`for`** loops inside one another to iterate over multi-dimensional data.
structures like lists of lists. Here's an example:

        matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

        for row in matrix:

                for element in row:
                        print(element, end=" ")
                print()


        # Output:
        # 1 2 3
        # 4 5 6
        # 7 8 9

In this example, the outer **`for`** loop iterates over each row in the **`matrix`** list, and the inner **`for`** loop iterates over each element within that row.

### 3. Python **`for`** loop with **`range()`** function:

The **`range()`** function is often used with **`for`** loops to iterate over a sequence of numbers. Here's an example:

        for i in range(5):
                print(i)


        # Output:
        # 0
        # 1
        # 2
        # 3
        # 4

In this example, the **`for`** loop iterates over the values generated by **`range(5)`**, which produces the sequence **`0`**, **`1`**, **`2`**, **`3`**, **`4`**.

### 4. **`break`** statement with **`for`** loop:

The **`break`** statement can be used to exit a **`for`** loop prematurely. Here's an example:

        numbers = [1, 2, 3, 4, 5]

        for num in numbers:

                if num == 3:
                        break
                print(num)


        # Output:
        # 1
        # 2

In this example, the **`for`** loop iterates over the **`numbers`** list, but when **`num`** becomes **`3`**, the **`break`** statement is executed, and the loop terminates.

### 5. **`continue`** statement with **`for`** loop:

The **`continue`** statement can be used to skip the current iteration and move to the next one. Here's an example:

        numbers = [1, 2, 3, 4, 5]

        for num in numbers:

                if num == 3:
                        continue
                print(num)


        # Output:
        # 1
        # 2
        # 4
        # 5

In this example, when **`num`** becomes **`3`**, the **`continue`** statement is executed, skipping the rest of the loop body for that iteration and moving to the next iteration.

### 6. Python **`for`** loop with an **`else`** block:

You can use an **`else`** block with a **`for`** loop, which is executed if the loop completes normally (without a **`break`** statement). Here's an example:

        numbers = [1, 2, 3, 4, 5]

        for num in numbers:
                print(num)

        else:
                print("Loop completed")


        # Output:
        # 1
        # 2
        # 3
        # 4
        # 5
        # Loop completed

In this example, the **`else`** block is executed after the **`for`** loop completes iterating over all the elements in the **`numbers`** list.

### 7. **`for`** loops using sequential data types:

Python's sequential data types, like strings, lists, tuples, and ranges, are all iterable, allowing you to use **`for`** loops to iterate over their elements. Here are some examples:

        # Iterating over a string
        for char in "Hello":
                print(char)


        # Iterating over a list
        numbers = [1, 2, 3, 4, 5]
        
        for num in numbers:
                print(num)

        
        # Iterating over a tuple
        point = (1, 2, 3)

        for coordinate in point:
                print(coordinate)


        # Iterating over a range
        for i in range(5):
                print(i)


### 8. Iterating through a dictionary:

While dictionaries are not sequences, you can use a **`for`** loop to iterate over their keys or key-value pairs. Here's an example:

        person = {"name": "Alice", "age": 25, "city": "New York"}

        # Iterating over keys
        for key in person:
                print(key)


        # Iterating over key-value pairs
        for key, value in person.items():
                print(f"{key}: {value}")

In this example, the first **`for`** loop iterates over the keys of the **`person`** dictionary, while the second **`for`** loop uses the **`items()`** method to iterate over the key-value pairs, unpacking them into the **`key`** and **`value`** variables during each iteration.

These examples cover various scenarios for using **`for`** loops in Python, including iterating over different data types, controlling loop flow with **`break`** and **`continue`**, and using the **`else`** block. The versatility of **`for`** loops makes them a powerful tool for working with sequences and iterables in Python.

</details>
<details><summary>Summary</summary> 
<br>

* The **`for`** loop is used to iterate over a sequence (list, tuple, string, or other iterable objects).
* The loop variable (e.g., **`item`** in the example above) takes on the value of each item in the sequence during each iteration.
* The loop body is executed once for each item in the sequence.
* The **`break`** statement can be used to exit the loop prematurely, and the **`continue`** statement can be used to skip the current iteration and move to the next one.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
