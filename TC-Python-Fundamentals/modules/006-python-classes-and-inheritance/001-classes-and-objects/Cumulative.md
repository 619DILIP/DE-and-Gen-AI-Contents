<details><summary>Learning Objectives</summary>
<br>

* Understand what classes and objects are in object-oriented programming.
* Be able to create a class and instantiate objects from it.
* Differentiate between class attributes, instance attributes, and methods.
* Be able to add methods to a class.

</details>
<details><summary>Description</summary>

## What is a class?

A class is a user-defined blueprint that encapsulates related data and behavior into a single entity. It serves as a template for creating objects, which are instances of that class. With a single class definition, you can instantiate multiple objects, each inheriting the properties and methods outlined within the class.

Python classes are composed of two types of attributes:

### Class Attributes:

* Shared by all instances: Class attributes belong to the class itself. A change in a class attribute affects all instances of that class.
* Defined outside of methods: They are declared directly within the class body but outside of any methods (including the `__init__` method).
* Common uses:
  * Constants related to the class.
  * Keeping track of the total number of instances created.

### Instance Attributes:

* **Specific to each object:** Instance attributes are unique to each object (or instance) of a class. Their values can vary between different objects of the same class.
* **Defined in the `__init__()` method:** Instance attributes are typically initialized within the constructor (`__init__`) of the class.
* **Represent object state:** Instance attributes store the data that defines the particular characteristics or state of a specific object.

In essence, a class defines the structure and behavior of objects, while objects are the actual instances created from that class, possessing the specified data and functionality.

## Create a class:

In Python, classes are defined using the `class` keyword, similar to how functions are defined using the `def` keyword. The class definition acts as a blueprint for creating objects, which are instances of that class.

**Syntax:**

```
class ClassName:
    """
    This is a docstring.
    It provides a brief description of the class.
    """
    # Class attributes and methods go here
    pass
```

In this structure:

* **`class ClassName:`** defines a new class named `ClassName`.
* **Docstring:** The triple-quoted string immediately following the class definition is called a docstring. While not mandatory, it is a recommended practice to include a docstring that describes the purpose and functionality of the class, improving code readability and maintainability.
* **Statements:** Within the class definition, you can define class attributes (variables) and methods (functions).
* **Pass:** It is used to indicate that this class is empty.

When a class is defined, Python creates a namespace for that class, where all its attributes and methods reside. This namespace is used to access the class members.

Additionally, Python provides a special method called `__init__()` (double underscores on both sides), which is a constructor method automatically called when an object is created from the class. This method is commonly used to initialize the object's attributes with desired values.

## `__init__()` method:

The `__init__` method is a special method in Python classes, automatically called when an object of the class is created. It is similar to constructors in other object-oriented programming languages like Java and C++. The `__init__` method is used to initialize the attributes of an object.

Here's an example:

```
class Person:
    def __init__(self, name, age):
        self.name = name  # Assigning the name attribute
        self.age = age    # Assigning the age attribute

# Creating an object
person1 = Person("Alice", 25)
print(person1.name)  # Output: Alice
print(person1.age)   # Output: 25
```

In this example, the `__init__` method takes two arguments (`name` and `age`) along with the `self` parameter. When an instance of the Person class is created (`person1 = Person("Alice", 25)`), the `__init__` method is automatically called, and the name and age attributes are initialized with the provided values.

## Self Parameter:

In Python, `self` is a reference to the current instance of a class. It is used to access and modify the attributes and methods of the class within the class itself. While `self` is a widely accepted convention, you can use any other name, but it is recommended to stick with `self` for better readability and consistency with Python's conventions. It's important to note that `self` is not a reserved keyword in Python; it's just a convention, and you can use any other name, but it's strongly recommended to follow these conventions for better readability and consistency.

**Syntax:**

```
class ClassName:
    def __init__(self, arg1, arg2):
        self.attr1 = arg1  # Assigning attribute using self
        self.attr2 = arg2

    def method_name(self, arg):
        # Access instance attributes using self
        result = self.attr1 + arg
        # Modify instance attributes using self
        self.attr2 = result
        # Return a value
        return self.attr2
```

These methods are designed to work with instances of the class. The `self` parameter refers to the current instance of the class and is used to access and modify the instance attributes.

## Constructors in Python:

A constructor is a special method used to create and initialize an object of a class. This method is defined within the class itself. It is automatically executed when an object is created, and its primary purpose is to declare and initialize the object's data members or instance variables.

The constructor contains a collection of statements that execute at the time of object creation, setting up the initial state of the object's attributes. For instance, when you execute `obj = Sample()`, Python recognizes that `obj` is an object of the Sample class and calls the constructor of that class to create and initialize the object.

In Python, object creation is divided into two parts: object creation and object initialization. Internally, the `__new__` method is responsible for creating the object, while the `__init__` method is used to initialize the object's attributes.

**Syntax:**

```
def __init__(self):
    # body of the constructor
```

Where,

* **def:** The keyword is used to define a function.
* **`__init__()` method:** It is a reserved method. This method gets called as soon as an object of a class is instantiated.
* **self:** The first argument `self` refers to the current object. It binds the instance to the `__init__()` method. It's usually named `self` to follow the naming convention.

Note: The `__init__()` method arguments are optional. We can define a constructor with any number of arguments.

### Types of Constructors:

In Python, there are three main types of constructors:

1. **Default Constructor:**
   * This is the constructor automatically provided by Python when no constructor is explicitly defined in the class.
   * It is an empty constructor without any parameters.
   * The default constructor is used to create an object without any initial values for the object's attributes.

2. **Non-Parameterized Constructor:**
   * This is a constructor defined without any parameters.
   * It is used to initialize the object's attributes with default or predefined values.
   * Although it doesn't take any arguments, it can still perform initialization tasks or call other methods within the class.

3. **Parameterized Constructor:**
   * This is a constructor that accepts one or more parameters.
   * The parameters are used to initialize the object's attributes with specific values passed during object creation.
   * Parameterized constructors allow for more flexible and customized object initialization based on the values provided.

It's important to note that in Python, there is no explicit syntax for defining different types of constructors. The constructor is always defined using the `__init__` method, and the number and types of parameters it accepts determine whether it is a default, non-parameterized, or parameterized constructor.

Here's an example illustrating the different types of constructors:

```
class Example:
    # Default Constructor
    def __init__(self):
        self.value = 0

    # Non-Parameterized Constructor
    def __init__(self):
        self.value = 10

    # Parameterized Constructor
    def __init__(self, value):
        self.value = value
```

In the above example, if no constructor is defined, Python automatically provides the default constructor. If the `__init__` method is defined without any parameters, it becomes a non-parameterized constructor. And if the `__init__` method has one or more parameters, it is considered a parameterized constructor.

## What is an Object?

An object is a concrete realization of a class, an instantiation of the blueprint defined by the class. It encapsulates a collection of data (attributes or variables) and associated operations (methods) that operate on that data. Objects are used to perform actions and represent real-world entities or concepts within a program.

Objects possess two fundamental characteristics: state and behavior. The state of an object is defined by its attributes, which are variables that hold data representing the object's properties or characteristics. The behavior of an object is defined by its methods, which are functions that describe the actions or operations that can be performed on or by the object, potentially modifying its state.

Every object in Python has three intrinsic properties:

1. **Identity:** Each object has a unique identity, distinct from other objects, which is established when the object is created and remains constant throughout its lifetime.
2. **State:** The state of an object encompasses the values of its attributes at a given point in time, representing its current condition or characteristics.
3. **Behavior:**
The behavior of an object is defined by the methods associated with its class, enabling the object to perform specific tasks or operations based on its state and the input provided.

To illustrate the concept of objects, classes, state, and behavior, let's consider an example based on the real-world entity of a "Person."

![Example](Images/class_and_object-python.png)

Class: Person

State: Name, Gender, Occupation  
Behavior: Work, Study

''' By defining the "Person" class with these states and behaviors, we can create multiple objects (instances) representing different individuals with their unique characteristics and actions. '''

Object 1: Jessa

State:  
Name: Jessa  
Gender: Female  
Occupation: Software Engineer  
Behavior:  
Work: She is employed as a software developer at ABC Company.  
Study: Jessa dedicates 2 hours per day to studying.

Object 2: Jon

State:  
Name: Jon  
Gender: Male  
Occupation: Doctor  
Behavior:  
Work: He practices medicine as a doctor.  
Study: Jon devotes 5 hours per day to studying.

In this example, Jessa and Jon are two distinct objects created from the same "Person" class. While they share the same class blueprint, they possess different states (attribute values) and exhibit unique behaviors based on their respective occupations and study habits.

Despite being instantiated from the same class, Jessa is a female software engineer who works at a company and studies for 2 hours daily, while Jon is a male doctor who practices medicine and studies for 5 hours per day.

This exemplifies how classes serve as templates for creating objects, each with its own specific state and behavior, allowing for the modeling of real-world entities and scenarios within a programming context.

## Create an Object:

Objects are essential for accessing and manipulating the attributes and methods defined within a class.

To create an object, you use the class name followed by parentheses. This process is known as instantiation, and the resulting object is an instance of that class.

__Syntax:__

object_name = ClassName()

In Python, object creation is divided into two parts: object creation and object initialization.

1. Object Creation:  
* Internally, the `__new__` method is responsible for creating the object instance.  
2. Object Initialization:  
* The `__init__` method is a special method used to initialize the object with desired values or perform any necessary setup operations.  
* This method is automatically called when an object is created, and it allows you to provide arguments to set the initial state of the object.

After creating an object, you can verify if it is an instance of a particular class using the following methods:

* `type(object_name):` This built-in function returns the type (class) of the object.  
* `isinstance(object_name, ClassName):` This built-in function returns `True` if the object is an instance of the specified class (`ClassName`), and `False` otherwise.

By creating objects from classes, you can work with the attributes and methods defined within the class, allowing you to model and manipulate real-world entities or concepts within your Python program.

</details>

<details><summary>Real World Application</summary>
<br>

The real-world applications that leverage OOP principles are vast and diverse. Web development frameworks like Django and Flask heavily rely on classes and objects to provide a structured approach to building web applications. Similarly, game development engines such as Pygame employ OOP to create interactive and immersive gaming experiences. Even in the realm of scientific computing, libraries like NumPy and SciPy utilize these concepts to handle and manipulate large datasets efficiently.

By fully comprehending classes and objects, you'll unlock the ability to design and implement robust software solutions that adhere to industry best practices. These principles foster code reusability, encapsulation, and abstraction, enabling you to tackle complex problems with greater ease and efficiency. Ultimately, mastering OOP concepts in Python will equip you with the skills necessary to contribute to a wide range of software projects, from web applications to scientific simulations and beyond.

</details>
<details><summary>Implementation</summary> 
<br>

In Python, every class consists of two fundamental components: attributes and methods.

## Attributes:

Attributes are the properties or characteristics that define the state or qualities of an object. They differentiate one object from another within the same class. Attributes are declared as variables within a class, and each object can have its own unique values for these variables.

There are two types of attributes:

### Class Attribute: 
These attributes are shared among all instances of the class. There is only one copy of a class attribute, and any modifications made to it will be reflected across all instances.
```Python
        class Player:
            team_name = "Dragons"  # Class attribute

            def __init__(self, name):
                self.name = name

        player1 = Player("Alice")
        player2 = Player("Bob")

        print(player1.team_name)  # Output: Dragons
        print(player2.team_name)  # Output: Dragons
```
Let's break down the code step-by-step:

*Class Definition*

* __class Player:__ This line defines a class named 'Player'. Classes are blueprints for creating objects.
* __team_name = "Dragons" # Class attribute__ This is a class attribute. 
  Key points:
  * __Scope:__ Belongs to the __Player__ class itself and not to individual objects of the class.
  * __Shared:__ All instances (objects) of the __Player__ class will share the same value for __team_name__.
* __def __ __init__ __ (self, name):__ This is the constructor method of the Player class. It's a special method called when you create a new object.
  * __self:__ The first argument self always refers to the current object being created.
  * __self.name=name__ This creates an instance attribute called __name__ specific to each player object and assigns the value passed in the __name__ parameter to it.

*Object Creation and Accessing Attributes*

* __player1 = Player("Alice")__  This creates a __Player__ object named __player1__ and the constructor assigns "Alice" to the __`player1.name`__ instance attribute.
* __player2 = Player("Bob")__  This creates another __Player__ object called __player2__ and assigns "Bob"  to the __`player2.name`__ instance attribute.
* __print(player1.team_name)__
  * Accesses the class attribute __team_name__ through the __player1__ object. Since it's a class attribute, it holds the value "Dragons".
* __print(player2.team_name)__
  * Accesses the same class attribute __team_name__ through __player2__. The output will also be "Dragons".



### Instance Attribute: 
These attributes are specific to each instance (object) of the class. Every object has its own copy of instance attributes, and any changes made to these attributes affect only that particular object. 
```Python
        class Player:
            # ... (previous code) ...

            def __init__(self, name, score):
                self.name = name
                self.score = score

        player1 = Player("Alice", 100)
        player2 = Player("Bob", 50)

        print(player1.score)  # Output: 100
        print(player2.score)  # Output: 50
```
Let's break down the code step-by-step:

*Class Definition*

* __class Player:__  This defines a class named __Player__ which acts as a template for representing player objects.
* __def __ __init__ __ (self, name, score):__  This is the constructor method of the class. It has these key elements:
  * __self:__ Represents the individual instance (object) of the class being created.
  * __name__ and __score:__ Parameters used to provide initial data for the new object.
  * __self.name=name__ and __self.score=score__ These lines create and initialize instance attributes:
    * __`self.name:`__ An attribute to store the player's name.
    * __`self.score:`__ An attribute to store the player's score.

*Object Creation and Attribute Access*

* __player1 = Player("Alice", 100)__
  * Creates a new __Player__ object named __player1.__
  * The constructor __ __init__ __ is called, setting __`player1.name`__ to "Alice" and __player1.score__ to 100.
* __player2 = Player("Bob", 50)__
  * Creates a separate __Player__ object named __player2.__
  * Sets __`player2.name`__ to "Bob" and __player2.score__ to 50.
* ___print(player1.score)__  Accesses the score instance attribute of the player1 object, outputting 100.
* __print(player2.score)__  Accesses the score instance attribute of the player2 object, outputting 50.



## Create an object - Access, modify, and delete

Here’s an example for accessing, modifying, and deleting attributes and objects using the del keyword:
```Python
        class Person:
            def __init__(self, name, age):
                self.name = name
                self.age = age

        # Creating instances
        person1 = Person("Alice", 25)
        person2 = Person("Bob", 30)

        # Accessing attributes
        print(person1.name)  # Output: Alice
        print(person2.age)   # Output: 30

        # Modifying attributes
        person1.age = 26
        person2.name = "Robert"

        print(person1.age)   # Output: 26
        print(person2.name)  # Output: Robert

        # Deleting instance attributes
        del person1.age

        # Trying to access the deleted attribute will raise an AttributeError
        print(person1.age)  # Raises AttributeError: 'Person' object has no attribute 'age'

        # Deleting objects
        del person2

        # Trying to access the deleted object will raise a NameError
        print(person2.name)  # Raises NameError: name 'person2' is not defined
```
Let's break down this code step by step:

1. We define a __Person__ class with instance attributes __name__ and __age__.
2. We create two instances of the __Person__ class: __person1__ and __person2__.
3. We access the attributes of __person1__ and __person2__ using the dot notation.
4. We modify the age attribute of __person1__ and the __name__ attribute of __person2__ by assigning new values.
5. To delete an instance attribute, we use the __del__ keyword followed by the instance name and the attribute name: __del person1.age__. After deleting the __age__ attribute of __person1__, if we try to access it, Python will raise an __AttributeError__ because the attribute no longer exists for that instance.
6. To delete an entire object, we use the del keyword followed by the object name: __del person2__. After deleting __person2__, if we try to access any attribute of __person2__, Python will raise a __NameError__ because the object itself no longer exists.

In this example, we demonstrate how to access, modify, and delete instance attributes and objects using the del keyword.

* Accessing attributes is done using the dot notation: __instance.attribute_name__.
* Modifying attributes is done by assigning a new value to the attribute: __instance.attribute_name = new_value__.
* Deleting instance attributes is done using the del keyword: __del instance.attribute_name__.
* Deleting objects is also done using the del keyword: __del object_name__.

It's important to note that deleting an instance attribute only affects that specific instance, not other instances of the same class. Similarly, deleting an object only removes that particular instance from memory; it doesn't affect the class definition or other instances of the class.

By using the __del__ keyword, you can dynamically remove attributes or objects from your program's memory when they are no longer needed, freeing up resources and maintaining better memory management. However, be cautious when deleting attributes or objects, as attempting to access deleted entities will result in errors.

## Methods:

Methods define the behavior and functionality of a class. They are functions defined within a class that operate on instances of that class or the class itself.

There are two types of methods:

### Instance Methods: 
These methods operate on a specific instance of the class. They have access to the instance attributes and can modify them. Instance methods take the instance (__self__) as the first argument, allowing them to work with the instance's attributes and perform instance-specific operations.
```Python
        class Circle:
            def __init__(self, radius):
                self.radius = radius  # Instance attribute

            def area(self):  # Instance method
                return 3.14 * self.radius ** 2

        circle1 = Circle(5)
        print(circle1.area())  # Output: 78.5
```
Let's break down this code step by step:

*Class Definition*

* __class Circle:__ This defines a class called __Circle__, which serves as a blueprint for creating Circle objects.
* __def __init__(self, radius):__ This is the constructor method (__ __init__ __) of the class. It gets called automatically when a new __Circle__ object is created.
  * __self:__ The __self__ parameter represents the specific instance of the __Circle__ object that's being created.
  * __self.radius = radius:__ This line creates an instance attribute named __radius__ and assigns the value passed in the __radius__ parameter to it. This attribute will store the radius for each specific Circle object.
* __def area(self):__ This is an instance method called __area__. It's designed to calculate the area of a circle.
  * __self:__ Again, the __self__ parameter refers to the specific __Circle__ object on which the method is called.
  * __return 3.14 * self.radius ** 2:__ This line calculates the area (pi * radius squared) and returns the result. Notice how it accesses the __radius__ instance attribute using __self.radius__.

*Object Creation and Method Call*

* __circle1 = Circle(5)__ This creates a new __Circle__ object named __circle1__. The constructor (__ __init__ __) is called, setting the __circle1.radius__ attribute to 5.
* __print(circle1.area())__
  * __circle1.area():__ Calls the __area__ instance method on the __circle1__ object. Inside the method, __self__ refers to __circle1__.
  * The method calculates the area using the stored radius and returns the value.
  * The __print__ statement then displays the returned area to the console.

In this example, the __area__ method is an instance method of the __Circle__ class. It calculates and returns the area of the circle based on the __radius__ instance attribute.



### Class Methods: 
These methods operate on the class itself, rather than individual instances. They can access and modify class attributes, but not instance attributes. Class methods are decorated with __@classmethod__ and take the class (__cls__) as the first argument.
```Python
        class Student:
            school_name = "ABC School"  # Class attribute

        @classmethod
        def change_school_name(cls, new_name):
            cls.school_name = new_name

        Student.change_school_name("XYZ School")
        print(Student.school_name)  # Output: XYZ School
```
Let's break down this code step by step:

*Class Definition*

* __class Student:__ This defines a class called __Student__, representing a blueprint for creating student objects.
* __school_name = "ABC School" # Class attribute__ This is a class attribute. All __Student__ objects will share this attribute, indicating the default school name.

*Class Method*

* __@classmethod__ This decorator signifies that the following method is a class method. Class methods are bound to the class itself, not a specific instance.
* __def change_school_name(cls, new_name):__
  * __cls:__ Represents the __Student__ class itself. Class methods implicitly receive the class as their first parameter.
  * __new_name:__ This parameter takes the new school name you intend to assign.
  * __cls.school_name = new_name:__ This line directly modifies the class attribute __school_name__, updating it to the __new_name__ for all instances of the __Student__ class.

*Calling the Class Method*

* __Student.change_school_name("XYZ School")__  Calls the class method directly using the class name (__Student__). The value "XYZ School" is passed as the __new_name__ parameter.
* __print(Student.school_name)__  Accesses the __school_name__ class attribute, which has now been changed to "XYZ School" and will output this updated value.

In this example, the __change_school_name__ method is a class method of the __Student__ class. It modifies the __school_name__ class attribute for all instances of the __Student__ class.

</details>
<details><summary>Summary</summary> 
<br>

* Classes define new object types with their own attributes and methods
* Instance objects are created from the class blueprint
* Class attributes are shared by all instances
* Instance attributes are unique per object
* Methods can access and modify object instance data

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
