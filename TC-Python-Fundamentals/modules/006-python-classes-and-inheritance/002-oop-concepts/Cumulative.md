<details><summary>Learning Objectives</summary>
<br>

* Understand the fundamentals of OOP.
* Grasp the concepts of classes, objects, and their interactions.
* Master the four pillars: Abstraction, Encapsulation, Inheritance, and Polymorphism.
* Learn how to design and implement OOP solutions for real-world problems.
* Develop skills in writing modular, reusable, and maintainable OOP code.

</details>
<details><summary>Description</summary>
<br>

Object-Oriented Programming (OOP) is a programming paradigm that revolves around the concept of objects, which are instances of classes. It is designed to make code more modular, reusable, and easier to maintain by organizing it around real-world concepts or entities.

In OOP, data (attributes) and functions (methods) are encapsulated within objects, which represent specific instances of a class. This approach promotes code organization and modularity, as each object is responsible for its own data and behavior, making it easier to understand and maintain the codebase.

The four essential concepts of OOP are:

## Encapsulation: 
Encapsulation is a fundamental concept in object-oriented programming (OOP) that emphasizes the bundling of data and methods within a single unit, known as a class. It is a technique that provides controlled access to the internal components of an object, promoting data integrity, code organization, and maintainability.

The key aspects of encapsulation can be summarized as follows:

* **Information Hiding:** Encapsulation allows the concealment of the implementation details of an object's internal state and behavior from the outside world. This promotes code security and prevents unintended modifications or misuse of sensitive data and methods.
* **Access Control:** In Python, encapsulation is achieved through the use of access modifiers, which regulate the visibility and accessibility of class members (attributes and methods). Python uses naming conventions to indicate the intended access level of class members:
  * **Public members** are accessible from anywhere within the program.
  * **Private members**, denoted by a double underscore prefix (e.g., `__attribute` or `__method`), are intended for internal use within the class and are effectively private due to name mangling.
  * **Protected members**, denoted by a single underscore prefix (e.g., `_attribute` or `_method`), are intended for use within the class and its subclasses but are not strictly enforced by the language.
* **Controlled Interface:** Encapsulation promotes the creation of a well-defined interface for interacting with an object. By exposing only the necessary public methods and attributes, encapsulation allows developers to interact with the object in a controlled and predictable manner without directly accessing or modifying its internal state.
* **Code Organization and Maintainability:** By encapsulating related data and methods within a single class, encapsulation fosters code organization and improves code maintainability. It helps in separating concerns, making it easier to understand, modify, and extend the codebase.
* **Data Integrity:** Encapsulation helps in maintaining data integrity by providing a controlled access mechanism to the object's internal state. By restricting direct access to the object's attributes, encapsulation ensures that the data is modified only through the defined methods, preventing unintended or invalid changes that could compromise the object's integrity.

It's important to note that while Python does not enforce strict access control mechanisms like some other OOP languages, it relies on naming conventions and programmer discipline to follow the principles of encapsulation. Adhering to these conventions promotes code readability, maintainability, and collaboration among developers.

Encapsulation is a crucial aspect of OOP that enables the creation of robust, secure, and modular software systems. By encapsulating data and methods within classes and providing controlled access through well-defined interfaces, encapsulation promotes code reusability, extensibility, and overall code quality.

## Inheritance: 
Inheritance is a fundamental concept in Object-Oriented Programming (OOP) that allows a new class, known as a derived or child class, to inherit properties and behaviors from an existing class, called the parent or base class. This concept mirrors the real-life notion of inheritance, where offspring inherit characteristics from their parents.

Through inheritance, a derived class can acquire and utilize the attributes and methods of its parent class, enabling code reusability and promoting a hierarchical structure. This feature empowers programmers to build upon existing code instead of rewriting it from scratch, saving time and effort.

One of the key advantages of inheritance is its ability to model real-life relationships effectively. It provides a natural way to represent hierarchical relationships between objects, making the code more intuitive and easier to understand.

Inheritance also allows for the seamless extension of existing classes. Developers can create a derived class that inherits the core functionality from its parent class and then add additional features or modify specific behaviors without altering the original class. This promotes code maintainability and extensibility.

Furthermore, inheritance is transitive, meaning that if a class inherits from another class, any subclasses derived from the child class will automatically inherit the properties and behaviors of the parent class. This hierarchical nature allows for code organization and promotes code reuse at multiple levels.

In Python, there are several types of inheritance:

* **Single Inheritance:** In this type, a child class inherits from a single parent class, acquiring its attributes and methods.
* **Multi-level Inheritance:** This form of inheritance involves a child class inheriting from a parent class, which in turn inherits from another parent class, creating a multi-level hierarchy.
* **Hierarchical Inheritance:** In this case, multiple child classes inherit from a single parent class, allowing for the creation of a hierarchical structure with multiple branches.
* **Multiple Inheritance:** This type of inheritance allows a single child class to inherit from multiple parent classes, combining their attributes and methods.

## Polymorphism: 
Polymorphism, derived from the Greek words "poly" (many) and "morphs" (forms or shapes), is a concept that enables performing a single task or operation in multiple ways. It is a fundamental principle in Object-Oriented Programming (OOP) that promotes flexibility and extensibility in software design.

The essence of polymorphism can be illustrated through an analogy: imagine you want to navigate to the destination of Delhi. Typically, you would use a GPS navigation system, which can locate different routes leading to the same destination. Similarly, in programming, polymorphism allows for achieving a particular objective through various approaches or implementations.

In the OOP paradigm, polymorphism facilitates the execution of one task in several different ways. This concept is realized through two distinct mechanisms:

* **Compile-time Polymorphism (Method Overloading):** This form of polymorphism involves defining multiple methods within a class, sharing the same name but varying parameter lists (either in the number of parameters, their types, or both). The compiler determines which method to invoke based on the arguments provided during compilation. However, Python employs a different approach to achieve a similar effect, utilizing default parameter values and variable arguments (`*args` and `**kwargs`).
* **Runtime Polymorphism (Method Overriding):** Runtime polymorphism, also known as method overriding, occurs when a subclass provides its own implementation of a method that is already defined in its superclass. When an overridden method is called on an instance of the subclass, the subclass's implementation takes precedence, allowing for dynamic behavior based on the specific object type at runtime.

Polymorphism in Python OOP enables the treatment of objects from different classes as instances of a common superclass. This powerful concept allows code to be written in a generalized manner, capable of working with objects of multiple types, thereby enhancing flexibility and extensibility in software design.

Python achieves polymorphism primarily through method overriding, which is a form of runtime polymorphism. By allowing subclasses to override methods inherited from their superclasses with their own implementations, Python enables dynamic behavior based on the specific object type at runtime. Additionally, Python's ability to use default parameter values and variable arguments provides a limited form of compile-time polymorphism.

## Abstraction: 
Data abstraction is a fundamental principle in Object-Oriented Programming (OOP) that emphasizes hiding the intricate implementation details of an object and presenting only the essential features and functionalities to the user. While data abstraction and encapsulation are closely related concepts, they are distinct and serve different purposes in the OOP paradigm.

Abstraction is the process of representing complex systems or objects by focusing on their core functions and behaviors while omitting the underlying complexities and unnecessary information. It involves assigning meaningful names or identifiers to represent the essential operations or services provided by an object, without delving into the specifics of how those operations are carried out internally.
Encapsulation, on the other hand, is the mechanism that enables data abstraction by bundling the data and methods together within a class and providing controlled access to the object's internal state and behavior. Encapsulation ensures that the implementation details are hidden from the outside world, promoting information hiding and code security.

The primary goal of data abstraction is to shield users from the intricacies of code implementation, especially sensitive or complex details that are not relevant to the intended usage of the object. By exposing only the necessary information and functionalities, abstraction allows developers to concentrate on what an object does rather than how it does it, facilitating code reusability, maintainability, and modularity.

Some key aspects and benefits of data abstraction include:

* **Simplified Representation:** Abstraction presents a simplified view of an object or system, showcasing only the essential information and features required by the user, promoting ease of understanding and usage.
* **Abstract Classes and Methods:** In OOP, abstract classes are classes that cannot be instantiated but serve as blueprints for other classes to inherit from. These classes typically contain one or more abstract methods, which are method declarations without an implementation. Concrete subclasses that inherit from an abstract class must provide implementations for these abstract methods, enabling code reuse and extensibility.
* **Separation of Concerns:** Abstraction facilitates the separation of concerns by allowing developers to decompose complex systems into smaller, manageable components, each focusing on a specific aspect of the system, promoting code organization and maintainability.
* **Extensibility and Flexibility:** By exposing only the essential interfaces and hiding implementation details, abstraction enables the creation of new implementations or extensions without modifying existing code, fostering code reusability and facilitating the development of modular and scalable software systems.
* **Code Security:** Abstraction contributes to code security by concealing sensitive or implementation-specific details from the user, preventing unintended modifications or misuse of internal components.

It's important to note that while data abstraction is a conceptual principle focused on representing essential features and functionalities, encapsulation is the practical mechanism that enables abstraction by bundling data and methods together within a class and controlling access to the object's internal state and behavior through access modifiers (e.g., public, private, protected).

<br>

Python is an object-oriented programming language, meaning that it supports the principles of OOP. In Python, everything is an object, including functions and modules. Python's OOP features include classes, objects, inheritance, polymorphism, and other advanced concepts like metaclasses and multiple inheritance.

The modular nature of OOP in Python makes it ideal for developing various applications, from small scripts to large-scale software systems. By organizing code into objects and classes, developers can create reusable and maintainable code, promote code reuse through inheritance, and achieve abstraction through interfaces and abstract classes. Additionally, encapsulation helps in controlling access to data and methods, improving code security and reliability.

Overall, OOP in Python provides a powerful and flexible approach to software development, enabling developers to model real-world concepts and create robust, scalable, and maintainable applications.

</details>
<details><summary>Real World Application</summary>
<br>

* __Graphical User Interfaces (GUIs):__ Components like buttons, windows, menus, etc., are modeled as objects.
* __Simulation Software:__ Cars, airplanes, and weather systems can all be represented as objects with their own attributes and behaviors in a simulation.
* __Game Development:__ Characters, game items, and environments are frequently modeled using OOP principles.
* __Web Development:__ OOP can structure complex web applications, particularly on the backend.

</details>
<details><summary>Implementation</summary>
<br>

Here's a simple example of the four essential concepts of OOP:

## Encapsulation:

```
class Employee:
    def __init__(self, name, salary):
        # public member
        self.name = name
        # private member
        # not accessible outside of a class
        self.__salary = salary

    def show(self):
        print("Name is", self.name, "and salary is", self.__salary)

emp = Employee("Jessa", 40000)
emp.show()  # access salary from outside of a class
print(emp.__salary)
```

Output:

```
Name is Jessa and salary is 40000
AttributeError: 'Employee' object has no attribute '__salary'
```

Let's break down the code step-by-step:

1. **class Employee:** defines a new class named Employee.
2. **def __init__(self, name, salary):** is the constructor method, which is automatically called when creating a new instance of the Employee class. It takes two parameters: name and salary.
3. **self.name = name** creates a public instance variable name and assigns the value of the name parameter to it.
4. **self.__salary = salary** creates a private instance variable __salary and assigns the value of the salary parameter to it. The double underscore prefix (__) is a naming convention in Python to make a variable or method private, meaning it can only be accessed from within the class.
5. **def show(self):** defines a method named show within the Employee class.
6. **print("Name is", `self.name`, "and salary is", `self.__salary`)** inside the show method, it prints the values of the name and __salary instance variables.
7. **emp = Employee("Jessa", 40000)** creates a new instance of the Employee class with the name "Jessa" and a salary of 40000.
8. **emp.show()** calls the show method on the emp instance, which prints "Name is Jessa and salary is 40000".
9. **print(emp.__salary)** attempts to access the private __salary instance variable from outside the class, which raises an AttributeError because private members are not accessible from outside the class.

In this example, the **name** instance variable is public, meaning it can be accessed and modified from outside the class. However, the **__salary** instance variable is private, and it can only be accessed or modified from within the Employee class using methods like show.

Encapsulation protects the internal state of an object by hiding the implementation details from the outside world. It allows developers to control access to data and methods, ensuring data integrity and preventing unauthorized modifications. By making the **__salary** variable private, the code enforces that the salary can only be accessed or modified through the class methods, promoting code modularity and maintainability.

**Note:** In Python, we do not have access modifiers, such as public, private, and protected. But we can achieve encapsulation by using the prefix **single underscore** and **double underscore** to control access to variables and methods within the Python program.

## Abstraction:

```
from abc import ABC, abstractmethod

class Vehicle(ABC):
    @abstractmethod
    def start(self):
        pass

    @abstractmethod
    def stop(self):
        pass

class Car(Vehicle):
    def start(self):
        print("Starting the car engine.")

    def stop(self):
        print("Stopping the car engine.")

class Motorcycle(Vehicle):
    def start(self):
        print("Kick-starting the motorcycle.")

    def stop(self):
        print("Turning off the motorcycle.")

# Using the abstraction
car = Car()
car.start()  # Output: Starting the car engine.
car.stop()   # Output: Stopping the car engine.

motorcycle = Motorcycle()
motorcycle.start()  # Output: Kick-starting the motorcycle.
motorcycle.stop()   # Output: Turning off the motorcycle.
```

Let's break down the code step-by-step:

1. **from abc import ABC, abstractmethod** imports the **ABC** (Abstract Base Class) and the **abstractmethod** decorator from the **abc** module, which provides the infrastructure for defining abstract base classes in Python.
2. **class Vehicle(ABC):** defines an abstract base class named **Vehicle** that inherits from the **ABC** class.
3. **@abstractmethod** is a decorator that marks the **start** and **stop** methods as abstract methods.
4. **def start(self): pass** and **def stop(self): pass** define abstract methods **start** and **stop** within the **Vehicle** class. These methods have no implementation (the body is left empty with the pass statement), and they must be overridden by concrete subclasses.
5. **class Car(Vehicle):** defines a concrete subclass named **Car** that inherits from the **Vehicle** abstract base class.
6. **def start(self):** and **def stop(self):** override the abstract **start** and **stop** methods from the **Vehicle** class and provide concrete implementations for starting and stopping a car.
7. **class Motorcycle(Vehicle):** defines another concrete subclass named **Motorcycle** that also inherits from the **Vehicle** abstract base class.
8. **def start(self):** and **def stop(self):** override the abstract **start** and **stop** methods from the **Vehicle** class and provide concrete implementations for starting and stopping a motorcycle.
9. **car = Car()** creates an instance of the **Car** class.
10. **car.start()** and **car.stop()** call the **start** and **stop** methods of the **car** instance, respectively, and print the corresponding messages.
11. **motorcycle = Motorcycle()** creates an instance of the **Motorcycle** class.
12. **motorcycle.start()** and **motorcycle.stop()** call the **start** and **stop** methods of the **motorcycle** instance, respectively, and print the corresponding messages.
class acts as an abstraction, hiding the complex implementation details of starting and stopping different types of vehicles. It defines a common interface (`start` and `stop` methods) that concrete subclasses (`Car` and `Motorcycle`) must implement according to their specific requirements.

The user (or client code) interacts with the `Car` and `Motorcycle` objects through the common interface provided by the `Vehicle` class, without needing to know the inner workings of how each vehicle is started or stopped.

## Polymorphism:

 class Dog:
 def speak(self):
 return "Woof!"

 class Cat:
 def speak(self):
 return "Meow!"

 def animal_sound(animal):
 print(animal.speak())

 # Creating objects
 dog = Dog()
 cat = Cat()

 # Polymorphism in action
 animal_sound(dog)  # Output: Woof!
 animal_sound(cat)  # Output: Meow!

Let's break down the code step-by-step:

1. The `Dog` and `Cat` classes are defined, each with a `speak` method that returns the corresponding animal sound.
2. The `animal_sound` function takes an `animal` object as a parameter and calls its `speak` method, printing the result.
3. An instance of the `Dog` class (`dog`) and an instance of the `Cat` class (`cat`) are created.
4. The `animal_sound` function is called twice, once with the `dog` object and once with the `cat` object.
5. When `animal_sound(dog)` is called, the `speak` method of the `Dog` class is invoked, and it prints `"Woof!"`.
6. When `animal_sound(cat)` is called, the `speak` method of the `Cat` class is invoked, and it prints `"Meow!"`.

The key aspect of polymorphism in this example is that the `animal_sound` function can work with objects of different classes (`Dog` and `Cat`) as long as they have a `speak` method. The specific implementation of the `speak` method is determined at runtime based on the actual object's type.

This behavior is possible because both `Dog` and `Cat` classes have a `speak` method with the same name and signature (no parameters). When the `animal_sound` function calls the `speak` method on the `animal` object, Python automatically determines the correct implementation based on the object's type.

Polymorphism allows for code reusability and flexibility by enabling a single piece of code (in this case, the `animal_sound` function) to work with different types of objects, as long as they share a common interface (the `speak` method).

## Inheritance:

Python provides three types of inheritance:

### Single Inheritance:
In single inheritance, one class will inherit the properties of one class only.

 class Operations:
 a = 10
 b = 20
 def add(self):
 sum = self.a + self.b
 print("Sum of a and b is: ", sum)
 
 class MyClass(Operations):
 c = 50
 d = 10
 def sub(self):
 sub = self.c - self.d
 print("Subtraction of c and d is: ", sub)
 
 ob = MyClass()
 ob.add()
 ob.sub()

Output:

 Sum of a and b is: 30
 Subtraction of c and d is: 40

Let's break down the code step-by-step:

*The Operations Class*

* `a = 10` and `b = 20`: Two class variables named `a` and `b` are created and initialized with the values 10 and 20 respectively. These variables are accessible to all objects created from the `Operations` class.
* `def add(self):`
 * This defines a method named `add` within the `Operations` class. The `self` parameter refers to the specific object that calls this method.
 * `sum = self.a + self.b:` Inside the `add` method, a variable named `sum` is created. It calculates the sum of the object's `a` and `b` values (accessed using `self.a` and `self.b`).
 * `print("Sum of a and b is: ", sum):` This line prints a message to the console indicating the calculated sum.

*The MyClass Class*

* `class MyClass(Operations):`
 * This line defines a new class named `MyClass` and indicates that it inherits from the `Operations` class. This means `MyClass` gains all the variables and methods that were defined in the `Operations` class.
* `c = 50` and `d = 10:` Two new class variables, `c` and `d`, with values 50 and 10 are created within the `MyClass`.
* `def sub(self):`
 * This defines a method named `sub` inside the `MyClass`. Similar to the `add` method, `self` refers to the object calling the method.
 * `sub = self.c - self.d:` A variable named `sub` is created, calculating the difference between the object's `c` and `d` values.
 * `print("Subtraction of c and d is: ", sub):` This line prints a message indicating the calculated difference.

*Object Creation and Execution*

* `ob = MyClass()`
 * This creates an object named `ob` that is an instance of the `MyClass`. Because `MyClass` inherits from `Operations`, the `ob` object has access to `a`, `b`, `c`, `d` and the `add` and `sub` methods.
* `ob.add()`
 * Calls the `add` method (inherited from `Operations`) on the `ob` object. This prints "Sum of a and b is: 30".
* `ob.sub()`
 * Calls the `sub` method (defined in `MyClass`) on the `ob` object. This prints "Subtraction of c and d is: 40".

### Multilevel Inheritance:
In multilevel inheritance, one or more classes act as a base class, which means the second class will inherit the properties of the first class, and the third class will inherit the properties of the second class. So the second class will act as both the Parent class and the Child class.

 class Addition:
 a = 10
 b = 20
 def add(self):
 sum = self.a + self.b
 print("Sum of a and b is: ", sum)
 
 class Subtraction(Addition):
 def sub(self):
 sub = self.b - self.a
 print("Subtraction of a and b is: ", sub)
 
 class Multiplication(Subtraction):
 def mul(self):
 multi = self.a * self.b
 print("Multiplication of a and b is: ", multi)
 
 ob = Multiplication()
 ob.add()
 ob.sub()
 ob.mul()

Output:

 Sum of a and b is: 30
 Subtraction of a and b is: 10
 Multiplication of a and b is: 200

Let's break down the code step-by-step:

*Classes:*

* `Addition:`
 * `a = 10` and `b = 20:` Defines two class variables `a` and `b` with values 10 and 20.
 * `def add(self):`
 * Defines the `add` method which calculates the sum of `a` and `b` (`self.a + self.b`) and prints the result.
* `Subtraction(Addition):`
 * `class Subtraction(Addition):` Creates a class named `Subtraction` that inherits from `Addition`. This means it gains access to the `a`, `b`, and `add` properties and methods.
 * `def sub(self):`
 * Defines the `sub` method, which calculates the difference between `b` and `a` of the object (`self.b - self.a`) and prints the result.
* `Multiplication(Subtraction):`
 * `class Multiplication(Subtraction):` Creates a class named `Multiplication` that inherits from `Subtraction` (and therefore indirectly from `Addition` as well). This means it has access to all properties and methods defined in `Addition` and `Subtraction`.
 * `def mul(self):`
 * Defines the `mul` method, which calculates the product of `a` and `b` of the object (`self.a * self.b`) and prints the result.

*Object Creation and Execution:*

* `ob = Multiplication()`
 * Creates an object named `ob` of the `Multiplication` class.
* `ob.add()`
 * Calls the `add` method inherited from the `Addition` class. Prints "Sum of a and b is: 30".
* `ob.sub()`
 * Calls the `sub` method inherited from the `Subtraction` class. Prints "Subtraction of a and b is: 10".
* `ob.mul()`
 * Calls the `mul` method defined in the `Multiplication` class. Prints "Multiplication of a and b is: 200".

### Multiple Inheritance:
The class that inherits the properties of multiple classes is called Multiple Inheritance.

 class Addition:
 a = 10
 b = 20
 def add(self):
 sum = self.a + self.b
 print("Sum of a and b is: ", sum)
 
 class Subtraction():
 c = 50
 d = 10
 def sub(self):
 sub = self.c - self.d
 print("Subtraction of c and d is: ", sub)
 
 class Multiplication(Addition, Subtraction):
 def mul(self):
 multi = self.a * self.c
 print("Multiplication of a and c is: ", multi)
 
 ob = Multiplication()
 ob.add()
 ob.sub()
 ob.mul()

Output:

 Sum of a and b is: 30
 Subtraction of c and d is: 10
 Multiplication of a and c is: 500

Let's break down the code step-by-step:

*Classes*

* `Addition`
 * `a = 10` and `b = 20:` Defines class variables `a` and `b` with values 10 and 20.
 * `def add(self):`
 * Defines the `add` method, which calculates and prints the sum of the object's `a` and `b` values.
* `Subtraction`
 * `c = 50` and `d = 10:` Defines class variables `c` and `d` with values 50 and 10.
 * `def sub(self):`
 * Defines the `sub` method, which calculates and prints the difference between the object's `c` and `d` values.
* `Multiplication(Addition, Subtraction)`
 * `Inherits from both Addition and Subtraction:` This is where multiple inheritance occurs. `Multiplication` gains access to variables and methods from both parent classes.
 * `def mul(self):`
 * Defines the `mul` method, which calculates and prints the product of the object's `a` (from `Addition`) and `c` (from `Subtraction`) values.

*Object Creation and Execution*

* `ob = Multiplication()`
 * Creates an object `ob` of the `Multiplication` class.
* `ob.add()`
 * Calls the `add` method inherited from `Addition`. Prints "Sum of a and b is: 30".
* `ob.sub()`
 * Calls the `sub` method inherited from `Subtraction`. Prints "Subtraction of c and d is: 10".
* `ob.mul()`
 * Calls the `mul` method defined in `Multiplication`. Prints "Multiplication of a and c is: 500".

The `Multiplication` class inherits properties and behaviors from two separate classes (`Addition` and `Subtraction`). Python uses a specific order to determine which parent class's methods are used when there's ambiguity in multiple inheritance. You can check this order using `Multiplication.__mro__`.
* OOP is a programming paradigm that centers around objects, which encapsulate data and behavior. Its four pillars enable us to:
* Simplify complex systems by representing them with modular objects.
* Protect data through encapsulation.
* Create reusable code through inheritance.
* Achieve flexibility and adaptability through polymorphism.

</details>

<details><summary>Summary</summary>

# Summary 

* OOP is a programming paradigm that centers around objects, which encapsulate data and behavior. Its four pillars enable us to:
* Simplify complex systems by representing them with modular objects.
* Protect data through encapsulation.
* Create reusable code through inheritance.
* Achieve flexibility and adaptability through polymorphism.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
