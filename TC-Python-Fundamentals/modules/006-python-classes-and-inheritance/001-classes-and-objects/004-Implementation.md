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

