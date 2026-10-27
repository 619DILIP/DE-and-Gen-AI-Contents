<details><summary>Learning Objective</summary>
<br>

Understand and apply inheritance in Python to create hierarchical relationships between classes, enabling code reusability and promoting efficient structuring of object-oriented programs.
</details>

<details><summary>Description</summary>
<br>

Inheritance is a key concept in object-oriented programming (OOP) that allows a class (subclass or derived class) to inherit properties and methods from another class (superclass or base class). 

This promotes code reusability and establishes a hierarchical relationship between classes.
</details>

<details><summary>Real-World Application</summary>

### Inheritance in Python is commonly used for:

#### Code Reusability: 
* Avoiding redundant code by inheriting common attributes and behaviors from a superclass.

#### Hierarchical Organization:
* Creating a hierarchy of classes with specialized functionalities.

#### Polymorphism: 
* Implementing polymorphic behavior where subclasses can override superclass methods.
</details>

<details><summary>Implementation</summary>

### Creating a Base Class (Superclass):

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        raise NotImplementedError("Subclass must implement this method")
```
* In this code, a base class `Animal` is defined with an `__init__` constructor method to initialize the name attribute and a speak method. 
* The speak method raises a NotImplementedError to enforce that subclasses must implement their own speak method.

### Creating Subclasses (Derived Classes):

#### a. Single Inheritance:

```python
class Dog(Animal):
    def speak(self):
        return f"{self.name} says Woof!"
```
* Here, `Dog` is a subclass of `Animal` using single inheritance. 
* It overrides the speak method from the superclass to provide its own behavior of printing a woof message.

#### b. Multiple Inheritance:
  
```python
class Bird:
    def fly(self):
        return "Flying high"

class Parrot(Animal, Bird):
    def speak(self):
        return f"{self.name} says Squawk!"
```
* The `Parrot` class demonstrates multiple inheritance from both `Animal` and `Bird`.
* It inherits attributes and methods from both classes, and in this case, it overrides the speak method from `Animal` to print a squawk message.

### Using Inherited Methods:

```python
dog = Dog("Buddy")
print(dog.speak())  # Output: "Buddy says Woof!"

parrot = Parrot("Polly")
print(parrot.speak())  # Output: "Polly says Squawk!"
```
* Instances of `Dog` and `Parrot` are created, and their speak methods are called. 
* Since these methods are inherited from the superclass (`Animal`), they execute the overridden versions specific to each subclass.

### Checking Class Hierarchy:

```python
print(issubclass(Dog, Animal))  # Output: True
print(issubclass(Parrot, Bird))  # Output: True
```

* The `issubclass()` function checks the class hierarchy. 
* It verifies that `Dog` is a subclass of `Animal` and that `Parrot` is a subclass of `Bird`, returning True for both cases.

### Overriding Methods:

```python
class Cat(Animal):
    def speak(self):
        return f"{self.name} says Meow!"

cat = Cat("Whiskers")
print(cat.speak())  # Output: "Whiskers says Meow!"
```
* The `Cat` class inherits from `Animal` and overrides the `speak()` method to provide a customized behavior of printing a meow message. 
* The cat object is then created, and its speak method is called to confirm the overridden behavior.
</details>

<details><summary>Summary</summary>
<br>

* Inheritance in Python allows a subclass to inherit attributes and methods from a superclass.

* It promotes code reusability, hierarchical organization, and polymorphic behavior.

* Single inheritance involves one superclass and one subclass, while multiple inheritance involves multiple superclasses and one subclass.

* Subclasses can override superclass methods to provide specialized behavior.

* Class hierarchy can be checked using built-in functions like `issubclass()`.
</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
