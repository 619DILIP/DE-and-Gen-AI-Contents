Dictionaries in Python are a built-in data structure that allow you to store and organize data in the form of key-value pairs. They provide an efficient way to associate values with unique keys, making it easy to retrieve and manipulate data.

Dictionaries are useful for storing related data, such as information contained in an ID or a user profile. They are constructed using curly braces __{}__, with each key-value pair separated by a colon (__:__), and pairs separated by commas (__,__).

__Syntax:__

        my_dict = {
          "key1":"value1",
          "key2":"value2"
        }

Here's an example of a dictionary in Python:

        user_profile = {'name': 'Alice', 'age': 28, 'is_active': True, 'email': 'alice@example.com'}

In this example, the keys are __'name', 'age', 'is_active', and 'email',__ and their corresponding values are __'Alice', 28, True, and 'alice@example.com',__ respectively.

## What are Keys?

In dictionaries, keys play a crucial role in establishing a mapping between unique identifiers and their associated values, creating a map-like structure. Keys must be immutable data types, such as strings or numbers, because their values cannot change once assigned. This is a requirement to maintain the integrity of the mapping.

Mutable data types like lists cannot be used as keys because their values can change, violating the principle of immutability and making the mapping unreliable.

Within a single dictionary, keys must be unique. Duplicate keys are not allowed, and if a key is repeated, the subsequent entry will overwrite the previous value associated with that key. This ensures that each key maintains a one-to-one correspondence with its value.

The key acts as a connector between the unique identifier and its associated value, creating a map-like structure. If you were to remove the keys, you would be left with a simple data structure containing a sequence of values without any meaningful association or mapping.

Dictionaries hold key-value pairs at each position, where the key serves as the unique identifier, and the value represents the associated data. This mapping structure allows efficient storage, retrieval, and manipulation of data based on the unique keys.



## Dictionary Methods:

The Python dictionary provides a variety of methods and functions that can be used to easily perform operations on the key-value pairs. Python dictionary methods are listed below:

* clear() -> Removes all the elements from the dictionary
* copy()  -> Returns a shallow copy of the specified dictionary
* fromkeys(seq, val) ->	Creates a new dictionary with keys from seq and val assigned to all the keys
* get(key) -> Returns the value of the specified key
* has_key() -> Returns True if the key exists in the dictionary, else returns False
* items() -> Returns a list of dictionary’s items in (key, value) format pairs
* keys() -> Returns a list containing all the keys in the dictionary
* pop(key) -> Removes and returns an element from a dictionary having the given key
* popitem() -> Removes and returns an arbitrary item (key, value).
* setdefault(key, val) -> Returns the corresponding value if the key is in the dictionary. If not, inserts the key with a value of val
* update() -> Updates the dictionary by adding key-value pair
* values() -> Returns a list containing all the values in the dictionary
