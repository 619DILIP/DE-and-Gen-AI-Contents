<details><summary>Learning Objectives</summary>
<br>

* Understand the concept of key-value pairs and how dictionaries store data.
* Learn how to create, access, modify, and delete elements in a dictionary.
* Explore the properties of keys and values in dictionaries.
* Understand the use cases and real-world applications of dictionaries.
* Gain experience in working with dictionaries through practice exercises.

</details>
<details><summary>Description</summary>
<br>

Dictionaries in Python are a built-in data structure that allows you to store and organize data in the form of key-value pairs. They provide an efficient way to associate values with unique keys, making it easy to retrieve and manipulate data.

Dictionaries are useful for storing related data, such as information contained in an ID or a user profile. They are constructed using curly braces `{}`, with each key-value pair separated by a colon (`:`), and pairs separated by commas (`,`).

__Syntax:__

 my_dict = {
 "key1": "value1",
 "key2": "value2"
 }

Here's an example of a dictionary in Python:

 user_profile = {'name': 'Alice', 'age': 28, 'is_active': True, 'email': 'alice@example.com'}

In this example, the keys are `'name'`, `'age'`, `'is_active'`, and `'email'`, and their corresponding values are `'Alice'`, `28`, `True`, and `'alice@example.com'`, respectively.

## What are Keys?

In dictionaries, keys play a crucial role in establishing a mapping between unique identifiers and their associated values, creating a map-like structure. Keys must be immutable data types, such as strings or numbers, because their values cannot change once assigned. This is a requirement to maintain the integrity of the mapping.

Mutable data types like lists cannot be used as keys because their values can change, violating the principle of immutability and making the mapping unreliable.

Within a single dictionary, keys must be unique. Duplicate keys are not allowed, and if a key is repeated, the subsequent entry will overwrite the previous value associated with that key. This ensures that each key maintains a one-to-one correspondence with its value.

The key acts as a connector between the unique identifier and its associated value, creating a map-like structure. If you were to remove the keys, you would be left with a simple data structure containing a sequence of values without any meaningful association or mapping.

Dictionaries hold key-value pairs at each position, where the key serves as the unique identifier, and the value represents the associated data. This mapping structure allows efficient storage, retrieval, and manipulation of data based on the unique keys.

## Dictionary Methods:

The Python dictionary provides a variety of methods and functions that can be used to perform operations on the key-value pairs easily. Python dictionary methods are listed below:

* `clear()` -> Removes all the elements from the dictionary.
* `copy()` -> Returns a shallow copy of the specified dictionary.
* `fromkeys(seq, val)` -> Creates a new dictionary with keys from `seq` and `val` assigned to all the keys.
* `get(key)` -> Returns the value of the specified key.
* `has_key()` -> Returns True if the key exists in the dictionary; otherwise, returns False.
* `items()` -> Returns a list of the dictionary’s items in `(key, value)` format pairs.
* `keys()` -> Returns a list containing all the keys in the dictionary.
* `pop(key)` -> Removes and returns an element from the dictionary having the given key.
* `popitem()` -> Removes and returns an arbitrary item (`key, value`).
* `setdefault(key, val)` -> Returns the corresponding value if the key is in the dictionary. If not, inserts the key with a value of `val`.
* `update()` -> Updates the dictionary by adding a key-value pair.
* `values()` -> Returns a list containing all the values in the dictionary.

</details>
<details><summary>Real World Application</summary>
<br>

* Storing and retrieving configuration settings.
* Representing complex data structures, such as database records or API responses.
* Implementing caching mechanisms.
* Building data models for web applications or games.
* Maintaining user profiles or user-specific data.
* Keeping track of inventory or stock management systems.

</details>
<details><summary>Implementation</summary> 
<br>

There are three ways to create a dictionary.

* __Using curly brackets:__ Dictionaries are created by enclosing the comma-separated key: value pairs inside the `{}` curly brackets. The colon `:` is used to separate the key and value in a pair.
* __Using `dict()` constructor:__ Create a dictionary by passing the comma-separated key: value pairs inside the `dict()`.
* __Using a sequence__ having each item as a pair (key-value).

Here’s an example:

 # Create a dictionary using {}
 employee = {"name": "John Doe", "age": 35, "department": "IT"}
 print(employee)
 # Output: {'name': 'John Doe', 'age': 35, 'department': 'IT'}

 # Create a dictionary using `dict()`
 customer = dict({"name": "Jane Smith", "city": "New York", "phone": 1234567890})
 print(customer)
 # Output: {'name': 'Jane Smith', 'city': 'New York', 'phone': 1234567890}

 # Create a dictionary from a sequence having each item as a pair
 product = dict([("name", "Laptop"), ("brand", "Dell"), ("price", 999.99)])
 print(product)
 # Output: {'name': 'Laptop', 'brand': 'Dell', 'price': 999.99}

 # Create a dictionary with mixed keys
 # First key is a string, and the second is an integer
 mixed_dict = {"fruit": "Apple", 1: "Banana"}
 print(mixed_dict)
 # Output: {'fruit': 'Apple', 1: 'Banana'}

 # Create a dictionary with a value as a list
 student = {"name": "Alice", "grades": [90, 85, 92]}
 print(student)
 # Output: {'name': 'Alice', 'grades': [90, 85, 92]}

We have:

1. Created a dictionary `employee` with keys `"name"`, `"age"`, and `"department"` using curly braces `{}`.
2. Created a dictionary `customer` with keys `"name"`, `"city"`, and `"phone"` using the `dict()` constructor.
3. Created a dictionary `product` from a sequence of tuples, where each tuple represents a key-value pair.
4. Created a dictionary `mixed_dict` with mixed keys, one being a string (`"fruit"`) and the other being an integer (`1`).
5. Created a dictionary `student` with a value that is a list (`"grades"`).

## Accessing elements of a Dictionary:

There are two different ways to access the elements of a dictionary.

1. Retrieve value using the key name inside the `[]` square brackets.
2. Retrieve value by passing the key name as a parameter to the `get()` method of a dictionary.

Here’s an example:

 # Create a dictionary named student
 student = {"name": "John Doe", "age": 20, "major": "Computer Science"}

 # Access value using key name in []
 print(student['name'])  # Output: 'John Doe'

 # Get key value using key name in `get()`
 print(student.get('age'))  # Output: 20

In this example, we have created a dictionary `student` with keys `"name"`, `"age"`, and `"major"`. We then demonstrate the two ways to access the values associated with these keys:

1. Using square brackets `[]` and the key name: `print(student['name'])` retrieves the value `'John Doe'` associated with the `"name"` key.
2. Using the `get()` method and passing the key name as a parameter: `print(student.get('age'))` retrieves the value `20` associated with the `"age"` key.

Both methods allow you to access the values stored in a dictionary by providing the corresponding key. The `get()` method is useful when you want to provide a default value in case the key is not found in the dictionary, preventing a `KeyError` from being raised.

## Modify elements of a Dictionary:

Dictionaries in Python are mutable, which means their contents can be changed after they are created. We can add new key-value pairs or modify the values associated with existing keys using assignment operators. Additionally, Python provides the `update()` method to update or add multiple key-value pairs to a dictionary at once.

__Note:__ If the key-value pair already exists in the dictionary, the value is updated. If the key is not present, a new key-value pair is added to the dictionary.

Here’s an example:

 # To update/add elements in a dictionary
 fruits = {'Apple': 5, 'Banana': 3, 'Orange': 2}
 print('Original Dictionary:', fruits)

 # Updating the value of an existing key
 fruits['Banana'] = 7
 print('Updated Dictionary:', fruits)

 # Adding a new key-value pair
 fruits['Kiwi'] = 10
 print('Updated Dictionary:', fruits)

 # Using the `update()` method
 fruits.update({'Grape': 8, 'Mango': 6})
 print('Updated Dictionary:', fruits)

Output:

 Original Dictionary: {'Apple': 5, 'Banana': 3, 'Orange': 2}
 Updated Dictionary: {'Apple': 5, 'Banana': 7, 'Orange': 2}
 Updated Dictionary: {'Apple': 5, 'Banana': 7, 'Orange': 2, 'Kiwi': 10}
 Updated Dictionary: {'Apple': 5, 'Banana': 7, 'Orange': 2, 'Kiwi': 10, 'Grape': 8, 'Mango': 6}

In this example, we have a dictionary `fruits` with keys `'Apple'`, `'Banana'`, and `'Orange'`.

1. We update the value associated with the existing key `'Banana'` from `3` to `7` using the assignment operator `fruits['Banana'] = 7`.
2. We add a new key-value pair `'Kiwi': 10` by assigning a value to the new key `'Kiwi'`.
3. We use the `update()` method to add multiple key-value pairs at once. `fruits.update({'Grape': 8, 'Mango': 6})` adds the key-value pairs `'Grape': 8` and `'Mango': 6` to the `fruits` dictionary.

The output shows the original dictionary, the dictionary after updating the value of an existing key, the dictionary after adding a new key-value pair, and the final dictionary after using the `update()` method.

## Delete elements of a Dictionary:

A dictionary in Python provides several methods to remove elements, including removing individual entries, all entries, or the entire dictionary itself.

1. The `pop()` 
method can be used to remove a single element. It takes the key as an argument and returns the corresponding value. If the key is not found, it raises a __KeyError__.
2. The __popitem()__ method randomly removes and returns an arbitrary key-value pair from the dictionary as a tuple. If the dictionary is empty, it raises a __KeyError__.
3. The __clear()__ method removes all elements from the dictionary, leaving it empty.
4. The __del__ keyword is used to delete the entire dictionary completely.

Here’s an example:

 # To remove/delete elements from a dictionary
 student_grades = {'Alice': 90, 'Bob': 85, 'Charlie': 92, 'David': 88, 'Eve': 79}
 print('Original Dictionary:', student_grades)

 # removing a single element
 print('Removed value:', student_grades.pop('Bob'))
 print('Updated Dictionary:', student_grades)

 # Removing an arbitrary key-value pair
 print('Removed pair:', student_grades.popitem())
 print('Updated Dictionary:', student_grades)

 # removing all elements
 student_grades.clear()
 print('Dictionary after clearing:', student_grades)

 # deleting the dictionary itself
 del student_grades
 # print(student_grades)  # This will raise a NameError

Output:

 Original Dictionary: {'Alice': 90, 'Bob': 85, 'Charlie': 92, 'David': 88, 'Eve': 79}
 Removed value: 85
 Updated Dictionary: {'Alice': 90, 'Charlie': 92, 'David': 88, 'Eve': 79}
 Removed pair: ('Eve', 79)
 Updated Dictionary: {'Alice': 90, 'Charlie': 92, 'David': 88}
 Dictionary after clearing: {}

In this example, we have a dictionary student_grades with keys representing student names and values representing their grades.

1. We use __pop('Bob')__ to remove the key-value pair with the key __'Bob'__ and print the removed value (__85__).
2. We use __popitem()__ to remove and print an arbitrary key-value pair from the dictionary.
3. We use __clear()__ to remove all elements from the dictionary, leaving it empty.
4. We use the __del__ keyword to delete the entire dictionary __student_grades__. Attempting to access or print the dictionary after deletion will raise a __NameError__.

These methods provide flexibility in removing elements from a dictionary based on specific requirements, such as removing a particular key-value pair, removing all elements, or deleting the entire dictionary.

## Find the length of a dictionary:

To find the number of items (key-value pairs) in a dictionary, we can use the __len()__ function. Let's consider a dictionary named __employee__ with some employee information and find its length.

Here’s an example:

 employee = {"name": "John Doe", "age": 35, "department": "IT", "salary": 60000}

 # Count the number of key-value pairs in the dictionary
 print(len(employee))
 # output: 4

In this example, we have a dictionary __employee__ with keys __"name", "age", "department", and "salary"__. By using the __len()__ function and passing the dictionary __employee__ as an argument, we get the output __4__, which represents the number of key-value pairs present in the dictionary.

The __len()__ function is a built-in function in Python that can be used to count the number of items in various data structures, including dictionaries. When applied to a dictionary, it returns the number of key-value pairs contained within it.

## Iterating a dictionary:

We can iterate through a dictionary using a for loop and access the individual keys and their corresponding values. Let's see this with an example:

 student = {"name": "John Doe", "age": 20, "major": "Computer Science", "gpa": 3.8}

 # Iterating the dictionary using a for-loop
 print('key', ':', 'value')
 for key in student:
 print(key, ':', student[key])

 # Using items() method
 print('key', ':', 'value')
 for key, value in student.items():
 print(key, value)

Output:

 key : value
 name : John Doe
 age : 20
 major : Computer Science
 gpa : 3.8

 key : value
 name John Doe
 age 20
 major Computer Science
 gpa 3.8

In this example, we have a dictionary __student__ with keys __"name", "age", "major", and "gpa"__.

The first way to iterate through the dictionary is using a simple __for__ loop and accessing the values using the keys:

 for key in student:
 print(key, ':', student[key])

This will print out each key followed by its corresponding value.

The second way is to use the __items()__ method, which returns a view object containing the key-value pairs of the dictionary as tuples in a list:

 for key, value in student.items():
 print(key, value)

This will directly print out each key and its associated value on the same line.

Both methods allow us to iterate through the dictionary and access its key-value pairs, making it easier to work with and manipulate the data stored in the dictionary.

</details>
<details><summary>Summary</summary> 
<br>

Dictionaries are a powerful and flexible data structure in Python, providing a way to store and organize data in a key-value format. They offer efficient access to data based on unique keys, making them suitable for various applications, such as storing configuration settings, representing complex data structures, implementing caching mechanisms, and more. Dictionaries are easy to use and offer a wide range of operations for manipulating and accessing data.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
