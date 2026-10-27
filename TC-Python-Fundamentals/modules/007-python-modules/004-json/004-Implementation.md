# Implementation 

## Convert JSON to Dictionary
To convert a JSON to a Dictionary object you use the loads function. Keep in mind: JSONs are formatted strings.
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
Compatible data types for the loads function are:
- str
- bytes
- bytearray

## Convert Dictionary to JSON

To convert a Dictionary into a JSON you use the dumps function
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
The json module works with JSON and Dictionaries by default, but it has support for working with custom classes as well

## Custom JSON Encoder
To make your custom class compatible with the json dumps functions you have to create an encoder for your class.
```python
import json

class MyClass:
    def __init__(self, name, age):
        self.name = name
        self.age = age

# this class will be used in the dumps function
class MyEncoder(json.JSONEncoder):
    # make sure to implement a function called default
    def default(self, obj):
        if isinstance(obj, MyClass):
            # if the MyClass fields were not compatible with json then we would need to craft a
            # custom dictionary to return here
            return obj.__dict__
        # return the result of the JSONEncoder default function if this encoder is used with
        # an incompatible class
        return super().default(obj)

my_obj = MyClass("Bob", 30)

my_json = json.dumps(my_obj, cls=MyEncoder)

print(my_json)
# output: {"name": "Bob", "value": 30}
```

## Custom JSON Decoder
Similar to the custom encoder, you will need to create a custom decoder if you want to convert a JSON into your custom class instead of a Dictionary, but you will use a function instead of a class
```python
import json

class MyClass:
    def __init__(self, name, age):
        self.name = name
        self.age = age
        
    def __str__(self) -> str:
        return f'MyClass(name={self.name}, age={self.age})'

# this function will be used to convert JSON data into a MyClass object
def from_json(json_data):
    # this checks if the json_data dictionary has both 'name' and 'age' keys
    if 'name' in json_data and 'age' in json_data:
        # this creates an object of MyClass and returns it with fields initialized
        return MyClass(json_data['name'], json_data['age'])
    # this returns the json_data dictionary if it doesn't have both 'name' and 'age' keys
    return json_data

json_data = '{"name": "Sally", "age": 30}'

# the object_hook parameter is used to tell the json.loads function to use the from_json function
# to convert the JSON data into a MyClass object, if it can
my_object = json.loads(json_data, object_hook=from_json)
print(my_object)
# output: MyClass(name=Sally, age=30)
```
