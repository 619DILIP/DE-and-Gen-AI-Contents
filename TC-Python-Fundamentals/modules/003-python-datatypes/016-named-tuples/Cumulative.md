# Cumulative for named tuples

<details><summary>Learning Objectives</summary>

# Learning Objectives
After completing this module, associates should be able to:

- Explain what a **`namedtuple`** is and why it is useful
- Create `namedtuple` types and instantiate them
- Access fields using **dot notation** instead of index positions
- Understand the differences between regular tuples and named tuples
- Use named tuples to create lightweight, immutable data structures

</details>

<details><summary>Description</summary>

# What is a `namedtuple`?

A **`namedtuple`** is a factory function from the `collections` module that creates **lightweight classes** whose instances behave like tuples **but with named fields**.

In other words:

- It’s a **tuple** → ordered, immutable, indexable  
- But also a **class** → fields can be accessed by *name*

Why use a named tuple?

- Improves **readability** (no more `item[0]`!)
- More **lightweight** than a full class
- Easier and faster to create than a traditional class
- Often used for simple records or structured data

They are perfect when you need a simple, immutable object with clearly named attributes.

</details>

<details><summary>Real World Application</summary>

# Real World Application for `namedtuple`

Named tuples help structure data without writing a full class.

### ✔️ Data modeling in small applications  
Represent coordinates, rectangles, ranges, or simple data items:

```python
Point = namedtuple("Point", ["x", "y"])
````

### ✔️ Rows from a database or file

Treat each row as a named container for clarity:

```python
Record = namedtuple("Record", ["id", "name", "email"])
```

### ✔️ API responses

When parsing JSON or API results, named tuples provide predictable attribute access.

### ✔️ Replacing dictionaries when immutability is required

Unlike dicts, named tuples are **immutable**, making them useful for:

* configuration values
* constants
* fixed records

Named tuples strike a balance between **clarity**, **performance**, and **simplicity**.

</details>

<details><summary>Implementation</summary>

# Implementation

## Importing `namedtuple`

```python
from collections import namedtuple
```

---

## Creating a Named Tuple Type

You first define the “class”:

```python
Point = namedtuple("Point", ["x", "y"])
```

Then you create instances:

```python
p = Point(10, 20)
```

---

## Accessing Fields by Name

Tuples normally use indexes:

```python
t = (10, 20)
print(t[0])  # 10
```

But with named tuples:

```python
p = Point(10, 20)
print(p.x)  # 10
print(p.y)  # 20
```

This makes code cleaner and more readable.

---

## Named Tuples Are Still Tuples

They support indexing:

```python
p[0]   # 10
p[1]   # 20
```

They also support unpacking:

```python
x, y = p
```

And they are immutable:

```python
p.x = 5   # ❌ Error — named tuples cannot be modified
```

---

## Creating Named Tuples with Defaults

Without defaults:

```python
Color = namedtuple("Color", ["r", "g", "b"])
```

With defaults (using `. _field_defaults`):

```python
Color = namedtuple("Color", ["r", "g", "b"], defaults=[0, 0, 0])
```

---

## Named Tuple Helper Methods

### `_replace()` — create a new modified copy

```python
new_point = p._replace(x=50)
```

### `_asdict()` — convert to a dictionary

```python
p._asdict()
```

Output:

```
{'x': 10, 'y': 20}
```

### `_fields` — show field names

```python
Point._fields  # ('x', 'y')
```

---

## Using `namedtuple` to Clean Up Code

### Without namedtuple:

```python
person = ("Alice", 30, "NYC")
name = person[0]    # Hard to read
```

### With namedtuple:

```python
Person = namedtuple("Person", ["name", "age", "city"])
person = Person("Alice", 30, "NYC")

print(person.name)  # Clear and readable
```

This is why named tuples are preferred in many real-world scripts and applications.

</details>

<details><summary>Summary</summary>

# Summary

* A **`namedtuple`** creates a tuple subclass with named fields.
* Instances behave like tuples: ordered, indexable, and immutable.
* Named fields allow clean attribute access with dot notation.
* Useful for lightweight, structured data without writing full classes.
* Provides helper methods like `_replace()`, `_asdict()`, and `_fields`.
* Ideal for small records, structured results, and simple data models.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>