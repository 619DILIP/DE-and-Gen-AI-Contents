# Implementation Creating a Dictionary:

There are following three ways to create a dictionary.

* __Using curly brackets:__ The dictionaries are created by enclosing the comma-separated Key: Value pairs inside the __{}__ curly brackets. The colon __`:`__ is used to separate the key and value in a pair.
* __Using dict() constructor:__  Create a dictionary by passing the comma-separated key: value pairs inside the dict().
* __Using sequence__ having each item as a pair (key-value)

Here’s an example:

    # Create a dictionary using {}
    employee = {"name": "John Doe", "age": 35, "department": "IT"}
    print(employee)
    # Output: {'name': 'John Doe', 'age': 35, 'department': 'IT'}

    # Create a dictionary using dict()
    customer = dict({"name": "Jane Smith", "city": "New York", "phone": 1234567890})
    print(customer)
    # Output: {'name': 'Jane Smith', 'city': 'New York', 'phone': 1234567890}

    # Create a dictionary from sequence having each item as a pair
    product = dict([("name", "Laptop"), ("brand", "Dell"), ("price", 999.99)])
    print(product)
    # Output: {'name': 'Laptop', 'brand': 'Dell', 'price': 999.99}

    # Create dictionary with mixed keys
    # First key is a string, and second is an integer
    mixed_dict = {"fruit": "Apple", 1: "Banana"}
    print(mixed_dict)
    # Output: {'fruit': 'Apple', 1: 'Banana'}

    # Create dictionary with value as a list
    student = {"name": "Alice", "grades": [90, 85, 92]}
    print(student)
    # Output: {'name': 'Alice', 'grades': [90, 85, 92]}

we have:

1. Created a dictionary __employee__ with keys __"name", "age", and "department"__ using curly braces __{}__.
2. Created a dictionary __customer__ with keys __"name", "city", and "phone"__ using the __dict()__ constructor.
3. Created a dictionary __product__ from a sequence of tuples, where each tuple represents a key-value pair.
4. Created a dictionary __mixed_dict__ with mixed keys, one being a string (__"fruit"__) and the other being an integer (__1__).
5. Created a dictionary __student__ with a value that is a list (__"grades"__).


## Accessing elements of a Dictionary:

There are two different ways to access the elements of a dictionary.

1. Retrieve value using the key name inside the __[]__ square brackets
2. Retrieve value by passing the key name as a parameter to the __get()__ method of a dictionary.

Here’s an example:

    # create a dictionary named student
    student = {"name": "John Doe", "age": 20, "major": "Computer Science"}

    # access value using key name in []
    print(student['name'])  # Output: 'John Doe'

    # get key value using key name in get()
    print(student.get('age'))  # Output: 20

In this example, we have created a dictionary __student__ with keys __"name", "age", and "major"__. We then demonstrate the two ways to access the values associated with these keys:

1. Using square brackets __[]__ and the key name: __print(student['name'])__ retrieves the value __'John Doe'__ associated with the __"name"__ key.
2. Using the __get()__ method and passing the key name as a parameter: __print(student.get('age'))__ retrieves the value __20__ associated with the __"age"__ key.

Both methods allow you to access the values stored in a dictionary by providing the corresponding key. The __get()__ method is useful when you want to provide a default value in case the key is not found in the dictionary, preventing a __KeyError__ from being raised.



## Modify elements of a Dictionary:

Dictionaries in Python are mutable, which means their contents can be changed after they are created. We can add new key-value pairs or modify the values associated with existing keys using assignment operators. Additionally, Python provides the __update()__ method to update or add multiple key-value pairs to a dictionary at once.

__Note:__ If the key-value pair already exists in the dictionary, the value is updated. If the key is not present, a new key-value pair is added to the dictionary.

Here’s an example:

    # To update/add elements in a dictionary
    fruits = {'Apple': 5, 'Banana': 3, 'Orange': 2}
    print('Original Dictionary:', fruits)

    # updating value of an existing key
    fruits['Banana'] = 7
    print('Updated Dictionary:', fruits)

    # adding a new key-value pair
    fruits['Kiwi'] = 10
    print('Updated Dictionary:', fruits)

    # using the update() method
    fruits.update({'Grape': 8, 'Mango': 6})
    print('Updated Dictionary:', fruits)

Output:

    Original Dictionary: {'Apple': 5, 'Banana': 3, 'Orange': 2}
    Updated Dictionary: {'Apple': 5, 'Banana': 7, 'Orange': 2}
    Updated Dictionary: {'Apple': 5, 'Banana': 7, 'Orange': 2, 'Kiwi': 10}
    Updated Dictionary: {'Apple': 5, 'Banana': 7, 'Orange': 2, 'Kiwi': 10, 'Grape': 8, 'Mango': 6}

In this example, we have a dictionary __fruits__ with keys __'Apple', 'Banana', and 'Orange'__.

1. We update the value associated with the existing key __'Banana'__ from __3__ to __7__ using the assignment operator __fruits['Banana'] = 7__.
2. We add a new key-value pair __'Kiwi': 10__ by assigning a value to the new key __'Kiwi'__.
3. We use the __update()__ method to add multiple key-value pairs at once. __fruits.update({'Grape': 8, 'Mango': 6})__ adds the key-value pairs __'Grape': 8__ and __'Mango': 6__ to the __fruits__ dictionary.

The output shows the original dictionary, the dictionary after updating the value of an existing key, the dictionary after adding a new key-value pair, and the final dictionary after using the __update()__ method.



## Delete elements of a Dictionary:

A dictionary in Python provides several methods to remove elements, including removing individual entries, all entries, or the entire dictionary itself.

1. The __pop()__ method can be used to remove a single element. It takes the key as an argument and returns the corresponding value. If the key is not found, it raises a __KeyError__.
2. The __popitem()__ method randomly removes and returns an arbitrary key-value pair from the dictionary as a tuple. If the dictionary is empty, it raises a __KeyError__.
3. The __clear()__ method removes all elements from the dictionary, leaving it empty.
4. The __del__ keyword is used to completely delete the entire dictionary.

Here’s an example:

    # To remove/delete elements from a dictionary
    student_grades = {'Alice': 90, 'Bob': 85, 'Charlie': 92, 'David': 88, 'Eve': 79}
    print('Original Dictionary:', student_grades)

    # removing a single element
    print('Removed value:', student_grades.pop('Bob'))
    print('Updated Dictionary:', student_grades)

    # removing an arbitrary key-value pair
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


## Find a length of a dictionary:

In order to find the number of items (key-value pairs) in a dictionary, we can use the __len()__ function. Let's consider a dictionary named __employee__ with some employee information and find its length.

Here’s an example:

    employee = {"name": "John Doe", "age": 35, "department": "IT", "salary": 60000}

    # count the number of key-value pairs in the dictionary
    print(len(employee))
    # output: 4

In this example, we have a dictionary __employee__ with keys __"name", "age", "department", and "salary"__. By using the __len()__ function and passing the dictionary __employee__ as an argument, we get the output __4__, which represents the number of key-value pairs present in the dictionary.

The __len()__ function is a built-in function in Python that can be used to count the number of items in various data structures, including dictionaries. When applied to a dictionary, it returns the number of key-value pairs contained within it.

## Iterating a dictionary:

We can iterate through a dictionary using a for-loop and access the individual keys and their corresponding values. Let's see this with an example:

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

