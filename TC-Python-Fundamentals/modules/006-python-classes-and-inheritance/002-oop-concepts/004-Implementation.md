# Implementation

Here’s a simple examples for the four essential concepts of OOP:

## Encapsulation:

    class Employee:
        def __init__(self, name, salary):
            # public member
            self.name = name
            # private member
            # not accessible outside of a class
            self.__salary = salary

        def show(self):
            print("Name is ", self.name, "and salary is", self.__salary)

    emp = Employee("Jessa", 40000)
    emp.show()  # access salary from outside of a class
    print(emp.__salary)

Output:

    Name is Jessa and salary is 40000
    AttributeError: 'Employee' object has no attribute '__salary'

Let's break down the code step-by-step:

1. **class Employee:** defines a new class named Employee.
2. **def __ __init__ __ (self, name, salary):** is the constructor method, which is automatically called when creating a new instance of the Employee class. It takes two parameters: name and salary.
3. **self.name=name** creates a public instance variable name and assigns the value of the name parameter to it.
4. **self.__salary = salary** creates a private instance variable _ _salary and assigns the value of the salary parameter to it. The double underscore prefix (__) is a naming convention in Python to make a variable or method private, meaning it can only be accessed from within the class.
5. **def show(self):** defines a method named show within the **Employee** class.
6. **print("Name is ", `self.name`, "and salary is", `self.__salary`)** inside the show method, it prints the values of the **name** and **__salary** instance variables.
7. **emp = Employee("Jessa", 40000)** creates a new instance of the **Employee** class with the name "Jessa" and a salary of 40000.
8. **emp.show()** calls the **show** method on the **emp** instance, which prints "Name is Jessa and salary is 40000".
9. **print(emp.__salary)** attempts to access the private **__salary** instance variable from outside the class, which raises an **AttributeError** because private members are not accessible from outside the class.

In this example, the **name** instance variable is public, meaning it can be accessed and modified from outside the class. However, the **__salary** instance variable is private, and it can only be accessed or modified from within the **Employee** class using methods like show.

Encapsulation protects the internal state of an object by hiding the implementation details from the outside world. It allows developers to control access to data and methods, ensuring data integrity and preventing unauthorized modifications. By making the **__salary** variable private, the code enforces that the salary can only be accessed or modified through the class methods, promoting code modularity and maintainability.

**Note:** In Python, we do not have access modifiers, such as public, private, and protected. But we can achieve encapsulation by using prefix **single underscore** and **double underscore** to control access of variable and method within the Python program.



## Abstraction:

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
    car.stop()  # Output: Stopping the car engine.

    motorcycle = Motorcycle()
    motorcycle.start()  # Output: Kick-starting the motorcycle.
    motorcycle.stop()  # Output: Turning off the motorcycle.

Let's break down the code step-by-step:

1. __from abc import ABC, abstractmethod__ imports the __ABC__ (Abstract Base Class) and the __abstractmethod__ decorator from the __abc__ module, which provides the infrastructure for defining abstract base classes in Python.
2. __class Vehicle(ABC):__ defines an abstract base class named __Vehicle__ that inherits from the __ABC__ class.
3. __@abstractmethod__ is a decorator that marks the __start__ and __stop__ methods as abstract methods.
4. __def start(self): pass__ and __def stop(self): pass__ define abstract methods __start__ and __stop__ within the __Vehicle__ class. These methods have no implementation (the body is left empty with the pass statement), and they must be overridden by concrete subclasses.
5. __class Car(Vehicle):__ defines a concrete subclass named __Car__ that inherits from the __Vehicle__ abstract base class.
6. __def start(self):__ and __def stop(self):__ override the abstract __start__ and __stop__ methods from the __Vehicle__ class and provide concrete implementations for starting and stopping a car.
7. __class Motorcycle(Vehicle):__ defines another concrete subclass named __Motorcycle__ that also inherits from the __Vehicle__ abstract base class.
8. __def start(self):__ and __def stop(self):__ override the abstract __start__ and __stop__ methods from the __Vehicle__ class and provide concrete implementations for starting and stopping a motorcycle.
9. __car = Car()__ creates an instance of the __Car__ class.
10. __car.start()__ and __car.stop()__ call the __start__ and __stop__ methods of the __car__ instance, respectively, and print the corresponding messages.
11. __motorcycle = Motorcycle()__ creates an instance of the __Motorcycle__ class.
12. __motorcycle.start()__ and __motorcycle.stop()__ call the __start__ and __stop__ methods of the __motorcycle__ instance, respectively, and print the corresponding messages.

In this example, the __Vehicle__ class acts as an abstraction, hiding the complex implementation details of starting and stopping different types of vehicles. It defines a common interface (__start__ and __stop__ methods) that concrete subclasses (__Car__ and __Motorcycle__) must implement according to their specific requirements.

The user (or client code) interacts with the __Car__ and __Motorcycle__ objects through the common interface provided by the __Vehicle__ class, without needing to know the inner workings of how each vehicle is started or stopped.


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

1. The __Dog__ and __Cat__ classes are defined, each with a __speak__ method that returns the corresponding animal sound.
2. The __animal_sound__ function takes an __animal__ object as a parameter and calls its __speak__ method, printing the result.
3. An instance of the __Dog__ class (__dog__) and an instance of the __Cat__ class (__cat__) are created.
4. The __animal_sound__ function is called twice, once with the __dog__ object and once with the __cat__ object.
5. When __animal_sound(dog)__ is called, the __speak__ method of the __Dog__ class is invoked, and it prints __"Woof!"__.
6. When __animal_sound(cat)__ is called, the __speak__ method of the __Cat__ class is invoked, and it prints __"Meow!"__.

The key aspect of polymorphism in this example is that the __animal_sound__ function can work with objects of different classes (__Dog__ and __Cat__) as long as they have a __speak__ method. The specific implementation of the __speak__ method is determined at runtime based on the actual object's type.

This behavior is possible because both __Dog__ and __Cat__ classes have a __speak__ method with the same name and signature (no parameters). When the __animal_sound__ function calls the __speak__ method on the __animal__ object, Python automatically determines the correct implementation based on the object's type.

Polymorphism allows for code reusability and flexibility by enabling a single piece of code (in this case, the __animal_sound__ function) to work with different types of objects, as long as they share a common interface (the __speak__ method).


## Inheritance:

Python provides three types of Inheritance:

### Single Inheritance: 
In Single inheritance, one class will inherit the properties of one class only.

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

* __a = 10__ and __b = 20:__  Two class variables named __a__ and __b__ are created and initialized with the values 10 and 20 respectively. These variables are accessible to all objects created from the __Operations__ class.
* __def add(self):__
  * This defines a method named add within the __Operations__ class. The __self__ parameter refers to the specific object that calls this method.
  * __sum = self.a + self.b:__ Inside the __add__ method, a variable named __sum__ is created. It calculates the sum of the object's __a__ and __b__ values (accessed using __self.a__ and __self.b__).
  * __print("Sum of a and b is: ", sum):__ This line prints a message to the console indicating the calculated sum.

*The MyClass Class*

* __class MyClass(Operations):__
  * This line defines a new class named __MyClass__ and indicates that it inherits from the __Operations__ class. This means __MyClass__ gains all the variables and methods that were defined in the __Operations__ class.
* __c = 50 and d = 10:__  Two new class variables, __c__ and __d__, with values 50 and 10 are created within the __MyClass__.
* __def sub(self):__
  * This defines a method named __sub__ inside the __MyClass__. Similar to the __add__ method, __self__ refers to the object calling the method.
  * __sub = self.c - self.d:__ A variable named __sub__ is created, calculating the difference between the object's __c__ and __d__ values.
  * __print("Subtraction of c and d is: ", sub):__ This line prints a message indicating the calculated difference.

*Object Creation and Execution*

* __ob = MyClass()__
  * This creates an object named ob that is an instance of the __MyClass__. Because __MyClass__ inherits from __Operations__, the __ob__ object has access to __a, b, c, d__ and the __add__ and __sub__ methods.
* __ob.add()__
  * Calls the __add__ method (inherited from __Operations__) on the __ob__ object. This prints "Sum of a and b is: 30".
* __ob.sub()__
  * Calls the __sub__ method (defined in __MyClass__) on the __ob__ object. This prints "Subtraction of c and d is: 40".



### Multilevel Inheritance: 
In multilevel Inheritance, one or more class act as a base class.

Which means the second class will inherit the properties of the first class and the third class will inherit the properties of the second class. So the second class will act as both the Parent class as well as Child class.

    class Addition:
        a = 10
        b = 20
        def add(self):
            sum = self.a + self.b
            print("Sum of a and b is: ", sum)
 
    class Subtraction(Addition):
        def sub(self):
            sub = self.b-self.a
            print("Subtraction of a and b is: ", sub)
 
    class Multiplication(Subtraction):
        def mul(self):
            multi = self.a * self.b
            print("Multiplication of a and b is: ", multi)
 
    ob = Multiplication ()
    ob.add()
    ob.sub()
    ob.mul()

Output:

    Sum of a and b is: 30
    Subtraction of a and b is: 10
    Multiplication of a and b is: 200

Let's break down the code step-by-step:

*Classes:*

* __Addition:__
  * __a = 10__ and __b = 20:__ Defines two class variables __a__ and __b__ with values 10 and 20.
  * __def add(self):__
    * Defines the __add__ method which calculates the sum of __a__ and __b__ (__self.a + self.b__) and prints the result.
* __Subtraction(Addition):__
  * __class Subtraction(Addition):__ Creates a class named __Subtraction__ that inherits from __Addition__. This means it gains access to the __a, b,__ and __add__ properties and methods.
  * __def sub(self):__
    * Defines the __sub__ method, which calculates the difference between __b__ and __a__ of the object (__self.b - self.a__) and prints the result.
* __Multiplication(Subtraction):__
  * __class Multiplication(Subtraction):__ Creates a class named __Multiplication__ that inherits from __Subtraction__ (and therefore indirectly from __Addition__ as well). This means it has access to all properties and methods defined in __Addition__ and __Subtraction__.
  * __def mul(self):__
    * Defines the __mul__ method, which calculates the product of __a__ and __b__ of the object (__self.a * self.b__) and prints the result.

*Object Creation and Execution:*

* __ob = Multiplication()__
  * Creates an object named ob of the __Multiplication__ class.
* __ob.add()__
  * Calls the __add__ method inherited from the __Addition__ class. Prints "Sum of a and b is: 30".
* __ob.sub()__
  * Calls the __sub__ method inherited from the __Subtraction__ class. Prints "Subtraction of a and b is: 10".
* __ob.mul()__
  * Calls the __mul__ method defined in the __Multiplication__ class. Prints "Multiplication of a and b is: 200".



### Multiple Inheritance: 
The class which inherits the properties of multiple classes is called Multiple Inheritance.

    class Addition:
        a = 10
        b = 20
        def add(self):
            sum = self. a+ self.b
            print("Sum of a and b is: ", sum)
 
    class Subtraction():
        c = 50
        d = 10
        def sub(self):
            sub = self.c-self.d
            print("Subtraction of c and d is: ", sub)
 
    class Multiplication(Addition,Subtraction):
        def mul(self):
            multi = self.a * self.c
            print("Multiplication of a and c is: ", multi)
 
    ob = Multiplication ()
    ob.add()
    ob.sub()
    ob.mul()

Output:

    Sum of a and b is: 30
    Subtraction of c and d is: 10
    Multiplication of a and c is: 500

Let's break down the code step-by-step:

*Classes*

* __Addition__
  * __a = 10__ and __b = 20:__ Defines class variables __a__ and __b__ with values 10 and 20.
  * __def add(self):__
    * Defines the __add__ method, which calculates and prints the sum of the object's __a__ and __b__ values.
* __Subtraction__
  * __c = 50__ and __d = 10:__ Defines class variables __c__ and __d__ with values 50 and 10.
  * __def sub(self):__
    * Defines the __sub__ method, which calculates and prints the difference between the object's __c__ and __d__ values.
* __Multiplication(Addition, Subtraction)__
  * __Inherits from both Addition and Subtraction:__ This is where multiple inheritance occurs. __Multiplication__ gains access to variables and methods from both parent classes.
  * __def mul(self):__
    * Defines the __mul__ method, which calculates and prints the product of the object's __a__ (from __Addition__) and __c__ (from __Subtraction__) values.

*Object Creation and Execution*

* __ob = Multiplication()__
  * Creates an object ob of the __Multiplication__ class.
* __ob.add()__
  * Calls the __add__ method inherited from __Addition__. Prints "Sum of a and b is: 30".
* __ob.sub()__
  * Calls the __sub__ method inherited from __Subtraction__. Prints "Subtraction of c and d is: 40".
* __ob.mul()__
  * Calls the __mul__ method defined in __Multiplication__. Prints "Multiplication of a and c is: 500"

The __Multiplication__ class inherits properties and behaviors from two separate classes (__Addition__ and __Subtraction__). Python uses a specific order to determine which parent class's methods are used when there's ambiguity in multiple inheritance. You can check this order using **Multiplication.__ mro __**.