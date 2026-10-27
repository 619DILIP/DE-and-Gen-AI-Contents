# Cumulative for the JSON

<details><summary>Learning Objectives</summary>

# Learning Objectives
After completing this module, associates should be able to:
- Explain what the json module is
- Identify situations where using the json module would be beneficial
- Make use of the json module

</details>

<details><summary>Description</summary>

# Introduction 
JavaScript Object Notation (JSON) is one of the most common data formats used in programming. Fundamentally, JSON is simply a formatted string. Since just about every programming language has a way to interact with strings, it is an ideal format for transferring data between services. The Python library comes with a module called "json" that has helper functions for creating and decoding JSON.

JSON supports the following data types (represented in string form):
- string
- number
- boolean
- nested JSON (key: value pair collections)
- arrays
- null

</details>
<details><summary>Real World Application</summary>

# Real World Application for JSON
There are a myriad of programming languages in the world, and you can never be too certain of what particular language a service you work with uses. Because of this, JSON has become the standard format for transferring data between services since it is easy to work with strings. This means any time your application needs to send data to another location, it would be reasonable to transform that data into JSON format before sending it, allowing the receiving service to decode the data.

Likewise, setting up your application to receive data in JSON format prepares you for maximum compatibility with other services you may want to interface with in the future.

</details>
<details><summary>Implementation</summary>

# Implementation 

## Convert JSON to Dictionary
To convert a JSON to a Dictionary object, you use the `loads` function. Keep in mind: JSONs are formatted strings.
```python
import json

# note: the \ indicates the expression continues on the next line
some_json = \
"""
{
 "name": "Bob",
 "age": 40,
 "isEmployed": true,
 "petName": null
}
"""

json_to_dict = json.loads(some_json)

print(json_to_dict)
# output: {'name': 'Bob', 'age': 40, 'isEmployed': True, 'petName': None}

```
Compatible data types for the `loads` function are:
- str
- bytes
- bytearray

## Convert Dictionary to JSON

To convert a Dictionary into JSON, you use the `dumps` function.
```python
import json

some_dict = {
    "name": "Bob",
    "age": 40,
    "isEmployed": True,
    "petName": None
}


dict_to_json = json.dumps(some_dict)

print(dict_to_json)
# output: {"name": "Bob", "age": 40, "isEmployed": true, "petName": null}

```
The JSON module works with JSON and Dictionaries by default, but it also supports working with custom classes.

## Custom JSON Encoder
To make your custom class compatible with the `dumps` function, you have to create an encoder for your class.
```python
import json

class MyClass:
    def __init__(self, name, age):
        self.name = name
        self.age = age

# This class will be used in the dumps function
class MyEncoder(json.JSONEncoder):
    # Make sure to implement a function called default
    def default(self, obj):
        if isinstance(obj, MyClass):
            # If the MyClass fields were not compatible with JSON, then we would need to craft a
            # custom dictionary to return here
            return obj.__dict__
        # Return the result of the JSONEncoder default function if this encoder is used with
        # an incompatible class
        return super().default(obj)

my_obj = MyClass("Bob", 30)

my_json = json.dumps(my_obj, cls=MyEncoder)

print(my_json)
# output: {"name": "Bob", "age": 30}
```

## Custom JSON Decoder
Similar to the custom encoder, you will need to create a custom decoder if you want to convert a JSON into your custom class instead of a Dictionary, but you will use a function instead of a class.
```python
import json

class MyClass:
    def __init__(self, name, age):
        self.name = name
        self.age = age
        
    def __str__(self) -> str:
        return f'MyClass(name={self.name}, age={self.age})'

# This function will be used to convert JSON data into a MyClass object
def from_json(json_data):
    # This checks if the json_data dictionary has both 'name' and 'age' keys
    if 'name' in json_data and 'age' in json_data:
        # This creates an object of MyClass and returns it with fields initialized
        return MyClass(json_data['name'], json_data['age'])
    # This returns the json_data dictionary if it doesn't have both 'name' and 'age' keys
    return json_data

json_data = '{"name": "Sally", "age": 30}'

# The object_hook parameter is used to tell the json.loads function to use the from_json function
# to convert the JSON data into a MyClass object, if it can
my_object = json.loads(json_data, object_hook=from_json)
print(my_object)
# output: MyClass(name=Sally, age=30)
```

</details>
<details><summary>Summary</summary>

# Summary 

- The JSON module is used to work with JSON data easily.
- The `json` module converts JSONs into Dictionaries and vice versa by default.
- To convert a custom class into a JSON, you need a custom encoder.
- To convert a JSON into a custom class, you need a custom decoder.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
