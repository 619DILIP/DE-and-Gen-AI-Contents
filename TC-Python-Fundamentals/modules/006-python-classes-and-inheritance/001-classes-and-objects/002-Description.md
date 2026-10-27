## What is a class?

A class is a user-defined blueprint that encapsulates related data and behavior into a single entity. It serves as a template for creating objects, which are instances of that class. With a single class definition, you can instantiate multiple objects, each inheriting the properties and methods outlined within the class.

Python classes are composed of two types of attributes:

### Class Attributes:

* Shared by all instances: Class attributes belong to the class itself. A change in a class attribute affects all instances of that class.
* Defined outside of methods: They are declared directly within the class body but outside of any methods (including the __ __init__ __ method).
* Common uses:
  * Constants related to the class
  * Keeping track of the total number of instances created

### Instance Attributes:

* __Specific to each object:__ Instance attributes are unique to each object (or instance) of a class. Their values can vary between different objects of the same class.
* __Defined in the __ __init__ __ () method:__ Instance attributes are typically initialized within the constructor (__ __init__ __) of the class.
* __Represent object state:__ Instance attributes store the data that defines the particular characteristics or state of a specific object.

In essence, a class defines the structure and behavior of objects, while objects are the actual instances created from that class, possessing the specified data and functionality.

## Create a class:

In Python, classes are defined using the __class__ keyword, similar to how functions are defined using the def keyword. The class definition acts as a blueprint for creating objects, which are instances of that class.

__Syntax:__

        class ClassName:
                """
                This is a docstring.
                It provides a brief description of the class.
                """
                # Class attributes and methods go here
                pass

In this structure:

* __class ClassName:__ defines a new class named ClassName.
* __Docstring:__ The triple-quoted string immediately following the class definition is called a docstring. While not mandatory, it is a recommended practice to include a docstring that describes the purpose and functionality of the class, improving code readability and maintainability.
* __Statements:__ Within the class definition, you can define class attributes (variables) and methods (functions).
* __Pass:__ It is used to indicate that this class is empty.

When a class is defined, Python creates a namespace for that class, where all its attributes and methods reside. This namespace is used to access the class members.

Additionally, Python provides a special method called __ __init__ __ () (double underscores on both sides), which is a constructor method automatically called when an object is created from the class. This method is commonly used to initialize the object's attributes with desired values.

## __ __init__ __ () method:

The __ __init__ __ method is a special method in Python classes, which is automatically called when an object of the class is created. It is similar to constructors in other object-oriented programming languages like Java and C++. The __ __init__ __ method is used to initialize the attributes of an object.

Here's an example:

        class Person:
            def __init__(self, name, age):
                self.name = name  # Assigning the name attribute
                self.age = age  # Assigning the age attribute

        # Creating an object
        person1 = Person("Alice", 25)
        print(person1.name)  # Output: Alice
        print(person1.age)  # Output: 25

In this example, the __ __init__ __ method takes two arguments (__name__ and __age__) along with the __self__ parameter. When an instance of the Person class is created (__person1 = Person("Alice", 25)__), the __ __init__ __ method is automatically called, and the name and age attributes are initialized with the provided values.

## Self Parameter:

In Python, __self__ is a reference to the current instance of a class. It is used to access and modify the attributes and methods of the class within the class itself. While __self__ is a widely accepted convention, you can use any other name, but it's recommended to stick with __self__ for better readability and consistency with Python's conventions. It's important to note that __self__ is not a reserved keyword in Python; it's just a convention and you can use any other names, but it's strongly recommended to follow these conventions for better readability and consistency.

__Syntax:__

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

These methods are designed to work with instances of the class. The __self__ parameter refers to the current instance of the class and is used to access and modify the instance attributes.

## Constructors in python:

A constructor is a special method used to create and initialize an object of a class. This method is defined within the class itself. It is automatically executed when an object is created, and its primary purpose is to declare and initialize the object's data members or instance variables.

The constructor contains a collection of statements that execute at the time of object creation, setting up the initial state of the object's attributes. For instance, when you execute __obj = Sample()__, Python recognizes that __obj__ is an object of the Sample class and calls the constructor of that class to create and initialize the object.

In Python, object creation is divided into two parts: object creation and object initialization. Internally, the __ __new__ __ method is responsible for creating the object, while the __ __init__ __ method is used to initialize the object's attributes.

__Syntax:__

        def __init__(self):
            # body of the constructor

Where,

* __def:__ The keyword is used to define function.
* **__ __init__ __ () Method:** It is a reserved method. This method gets called as soon as an object of a class is instantiated.
* __self:__ The first argument self refers to the current object. It binds the instance to the __init__() method. It’s usually named self to follow the naming convention.

Note: The __ __init__ __ () method arguments are optional. We can define a constructor with any number of arguments.

### Types of Constructors:

In Python, there are three main types of constructors:

1. __Default Constructor:__
  * This is the constructor that is automatically provided by Python when no constructor is explicitly defined in the class.
  * It is an empty constructor without any parameters.
  * The default constructor is used to create an object without any initial values for the object's attributes.
2. __Non-Parameterized Constructor:__
  * This is a constructor that is defined without any parameters.
  * It is used to initialize the object's attributes with default or predefined values.
  * Although it doesn't take any arguments, it can still perform initialization tasks or call other methods within the class.
3. __Parameterized Constructor:__
  * This is a constructor that accepts one or more parameters.
  * The parameters are used to initialize the object's attributes with specific values passed during object creation.
  * Parameterized constructors allow for more flexible and customized object initialization based on the values provided.

It's important to note that in Python, there is no explicit syntax for defining different types of constructors. The constructor is always defined using the __ __init__ __ method, and the number and types of parameters it accepts determine whether it is a default, non-parameterized, or parameterized constructor.

Here's an example illustrating the different types of constructors:

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

In the above example, if no constructor is defined, Python automatically provides the default constructor. If the __ __init__ __ method is defined without any parameters, it becomes a non-parameterized constructor. And if the __ __init__ __ method has one or more parameters, it is considered a parameterized constructor.



## What is an Object?

An object is a concrete realization of a class, an instantiation of the blueprint defined by the class. It encapsulates a collection of data (attributes or variables) and associated operations (methods) that operate on that data. Objects are used to perform actions and represent real-world entities or concepts within a program.

Objects possess two fundamental characteristics: state and behavior. The state of an object is defined by its attributes, which are variables that hold data representing the object's properties or characteristics. The behavior of an object is defined by its methods, which are functions that describe the actions or operations that can be performed on or by the object, potentially modifying its state.

Every object in Python has three intrinsic properties:

1. __Identity:__ Each object has a unique identity, distinct from other objects, which is established when the object is created and remains constant throughout its lifetime.
2. __State:__ The state of an object encompasses the values of its attributes at a given point in time, representing its current condition or characteristics.
3. __Behavior:__ The behavior of an object is defined by the methods associated with its class, enabling the object to perform specific tasks or operations based on its state and the input provided.


To illustrate the concept of objects, classes, state, and behavior, let's consider an example based on the real-world entity of a "Person."

![Example](Images\class_and_object-python.png)

        Class: Person

            State: Name, Gender, Occupation
            Behavior: Work, Study

        ''' By defining the "Person" class with these states and behaviors, we can create multiple objects (instances) representing different individuals with their unique characteristics and actions. '''

        Object 1: Jessa

            State:
                Name: Jessa
                Gender: Female
                Occupation: Software Engineer
            Behavior:
                Work: She is employed as a software developer at ABC Company.
                Study: Jessa dedicates 2 hours per day to studying.

        Object 2: Jon

            State:
                Name: Jon
                Gender: Male
                Occupation: Doctor
            Behavior:
                Work: He practices medicine as a doctor.
                Study: Jon devotes 5 hours per day to studying.

In this example, Jessa and Jon are two distinct objects created from the same "Person" class. While they share the same class blueprint, they possess different states (attribute values) and exhibit unique behaviors based on their respective occupations and study habits.

Despite being instantiated from the same class, Jessa is a female software engineer who works at a company and studies for 2 hours daily, while Jon is a male doctor who practices medicine and studies for 5 hours per day.

This exemplifies how classes serve as templates for creating objects, each with its own specific state and behavior, allowing for the modeling of real-world entities and scenarios within a programming context.



## Create an Object:

Objects are essential for accessing and manipulating the attributes and methods defined within a class.

To create an object, you use the class name followed by parentheses. This process is known as instantiation, and the resulting object is an instance of that class.

__Syntax:__

        object_name = ClassName()

In Python, object creation is divided into two parts: object creation and object initialization.

1. Object Creation:
  * Internally, the __ __new__ __ method is responsible for creating the object instance.
2. Object Initialization:
  * The __ __init__ __ method is a special method used to initialize the object with desired values or perform any necessary setup operations.
  * This method is automatically called when an object is created, and it allows you to provide arguments to set the initial state of the object.

After creating an object, you can verify if it is an instance of a particular class using the following methods:

* __type(object_name):__ This built-in function returns the type (class) of the object.
* __isinstance(object_name, ClassName):__ This built-in function returns __True__ if the object is an instance of the specified class (__ClassName__), and __False__ otherwise.

By creating objects from classes, you can work with the attributes and methods defined within the class, allowing you to model and manipulate real-world entities or concepts within your Python program.

