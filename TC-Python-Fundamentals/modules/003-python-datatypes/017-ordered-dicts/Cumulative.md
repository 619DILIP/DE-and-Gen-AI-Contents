# Cumulative for OrderedDict

<details><summary>Learning Objectives</summary>

# Learning Objectives
After completing this module, associates should be able to:

- Explain what an **`OrderedDict`** is and how it differs from a normal dictionary
- Understand how dictionary ordering changed in modern Python versions
- Create and use `OrderedDict` objects from the `collections` module
- Use common methods like `move_to_end()` and `popitem()`
- Identify situations where `OrderedDict` is still useful today

</details>

<details><summary>Description</summary>

# What is an `OrderedDict`?

An **`OrderedDict`** is a dictionary subclass from the `collections` module that **remembers the order** in which keys were inserted.

Before Python 3.7:

- Regular dictionaries did **not** preserve insertion order.
- If you needed a dictionary that kept its order, you had to use `OrderedDict`.

After Python 3.7:

- Regular dictionaries **do** preserve insertion order by default.
- However, `OrderedDict` still provides **extra features** that normal dictionaries do not have.

Why use `OrderedDict` now?

- You need special order-related features (e.g., `move_to_end()`).
- You need predictable behavior across **older versions** of Python.
- You want ordered behavior explicitly for clarity in code.
- Some libraries/frameworks still rely on it.

</details>

<details><summary>Real World Application</summary>

# Real World Application for `OrderedDict`

Even though normal dictionaries preserve insertion order, `OrderedDict` remains helpful in several domains:

### ✔️ Caches and LRU behavior  
`move_to_end()` can quickly implement “most recently used” ordering.

### ✔️ Working with older Python (≤ 3.6)  
Legacy codebases and companies with long-lived systems still require it.

### ✔️ Ordered configuration or settings  
Sometimes you *want* to signal that the order is important.

### ✔️ Deterministic outputs  
When exporting JSON or writing files where order matters.

### ✔️ Maintaining order-related operations  
Such as reordering keys through `popitem()` or `move_to_end()`.

It’s still a valid tool when you need **explicit control** over key order.

</details>

<details><summary>Implementation</summary>

# Implementation

## Importing `OrderedDict`

```python
from collections import OrderedDict
```

---

## Creating an OrderedDict

```python
from collections import OrderedDict

od = OrderedDict()
od["first"] = 1
od["second"] = 2
od["third"] = 3

print(od)
```

Output:

```
OrderedDict([('first', 1), ('second', 2), ('third', 3)])
```

---

## Comparing to a Regular Dictionary

Modern Python:

```python
d = {}
d["first"] = 1
d["second"] = 2
d["third"] = 3

print(d)
```

Output (also preserves order):

```
{'first': 1, 'second': 2, 'third': 3}
```

So why use `OrderedDict`?

Because of its **extra methods**.

---

## Special Methods of `OrderedDict`

### `move_to_end()`

Moves a key to the end or beginning:

```python
od.move_to_end("second")     # moves "second" to end
od.move_to_end("second", last=False)  # moves to the beginning
```

### `popitem(last=True)`

Removes an item:

* `last=True` → removes the newest
* `last=False` → removes the oldest

```python
od.popitem()          # removes last item
od.popitem(last=False)  # removes first item
```

### `reversed()`

Iterate through keys in reverse insertion order:

```python
for key in reversed(od):
    print(key)
```

---

## Copying and Equality

Two `OrderedDict` objects are equal if:

* Their **keys and values** are equal
* Their **order** is the same

Example:

```python
OrderedDict([('a', 1), ('b', 2)]) == OrderedDict([('b', 2), ('a', 1)])  
# False — order matters
```

---

## Converting Between Types

### To a regular dict:

```python
regular = dict(od)
```

### From a regular dict (order preserved):

```python
od = OrderedDict({"x": 1, "y": 2, "z": 3})
```

---

## Practical Example: Simple LRU Cache Logic

```python
from collections import OrderedDict

cache = OrderedDict()

def access(key, value):
    cache[key] = value
    cache.move_to_end(key)   # mark as recently used

access("A", 1)
access("B", 2)
access("A", 3)  # “A” becomes most recently used

print(cache)
```

Output:

```
OrderedDict([('B', 2), ('A', 3)])
```

This would be much harder to express with a regular dictionary.

</details>

<details><summary>Summary</summary>

# Summary

* **`OrderedDict`** is a dictionary subclass that remembers insertion order.
* Before Python 3.7 it was necessary; now its value is in its **extra features**.
* Key methods include `move_to_end()` and `popitem()` for order-oriented logic.
* Useful for caches, deterministic output, older environments, or when explicit ordering is required.
* Behaves like a regular dictionary but with additional order-control tools.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>