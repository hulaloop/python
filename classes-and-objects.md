# Classes and objects

A class is a way to organize functions and data. Classes are used to create virtual objects like the `Turtle` you have been using in previous sections. 

You can think of a class as a template that defines what a object can do. For example, the `Turtle` class defines what turtles can do (move forward, turn, etc). Any number of `Turtle` objects can be created from it.

```
# Create two Turtle objects
a = Turtle()
b = Turtle()

# Each Turtle object moves independently
a.forward(100)
b.backward(100)
```

## Writing a class

Suppose a student is writing some `print` instructions to introduce themself. 

```python
print("My name is John.")
print("I am 14 years old.")
```

If another student wants to use this program, they will have to change `"John"` to their name, and `"14"` to their own age. If John had printed a longer introduction, it would have become more tedious for someone else to re-use his program.

John could also introduce himself by first creating a class that stores the information that all humans must have, like a name and an age.

```python
class Human:
  # description of a human
```

The description of a human can contain functions that define what a `Human` object can do. The first parameter to every function in a class is named `self`, which refers to the object performing the function.

```python
class Human:
  
  def introduce(self):
    print("My name is John")
    print("I am 14 years old")
```

When we create the class `Human`, we are also defining a special function named `Human` which creates a human object. This function is called a **constructor**, and it returns an object that can be stored in a variable.

Notice: the similarity between creating a `Human` object and creating a `Turtle` object.

```
john = Human()
john.introduce()
```

We can create multiple `Human` objects and introduce each of them, but they will all print out the same introduction.

```
john = Human()
jessica = Human()
mark = Human()

john.introduce()
jessica.introduce()
mark.introduce()
```

## Attributes

An object is really just a **reference** to a location in the computer's memory where data can be stored. In the case above, the `Human` constructor provides a memory location, and we saved it in the `john` variable. Each call to the `Human` constructor creates a new memory location for saving data, so the `jessica` and `mark` variables refer to different locations in the computer's memory.

Data that an object stores in its memory location is called an **attribute**, and can be used just like a variable. Objects are like dictionaries, and attributes are like key-value pairs.

Assign an attribute to an object
<diagram>
object.attribute = value
</diagram>

For example: humans have a `name` and `age` attribute. 

```
# Variables
name = "John"
age = 13

# Attributes
john = Human()
john.name = "John"
john.age = 13
```

When an object performs a function, the `self` variable refers to the object's memory location and allows us to access the object's attributes.

```
class Human:
  
  def introduce(self):
    print("My name is " + self.name)
    print("I am " + str(self.age) + " years old")
```

Now when we create two `Human` objects, we can set their attributes to different values so they introduce themselves uniquely.

```
mark = Human()
mark.name = "Mark"
mark.age = 15
mark.introduce()

jessica = Human()
jessica.name = "Jessica"
jessica.age = 12
jessica.introduce()
```

If an attribute has not been set, it's value will be the special value `None`. Using an attribute that has not been set will cause an error, so it is wise to check if an attribute has been set before using it.

```
class Human:
  def introduce(self):
    # Check if the name is set
    if self.name is None:
      print("I don't have a name yet.")
    else:
      print("My name is " + self.name)
      
    # Check if the age is set
    if self.age is not None:
      print("My age is " + str(self.age)
```

Problem: Vehicle class

Create a class `Vehicle` that has a `make` and `wheels` attribute.

- If the vehicle has 2 wheels, it is a motorcycle.
- If the vehicle has 4 wheels, it is a car.
- If the vehicle has more than 4 wheels, it is a truck.

Define a function `printType` which prints whether a `Vehicle` object is a motorcycle, car, or truck. For example, an object which has its `make` attribute set to `"Toyota"` should print an answer in the form `"I am a Toyota motorcycle"`, `"I am a Toyota car"`, or `"I am a Toyota truck"`.

Problem: Restaurant manager (something like this, TBD)

You are writing a program for a restaurant

```
r = Restaurant()
r.createPizza()
r.deliverPizza()
```

## Constructor

We can define a special function `__init__` that is called automatically when an object is created. In this function, you can initialize attributes and perform any setup steps for the object.

Notice: the double underscore on both sides of `init`.

```
class Human:
  def __init__(self):
    print("A human is born")

anonymous = Human()
```

In the `__init__` function, it is conventional to assign default values to the object's attributes. This allows us to use the attributes in another function without first checking if they contain `None`.

```
class Human:
  def __init__(self):
    print("A human is born")
    self.name = "Unknown"
    self.age = 0
```

## Parameters

The first parameter to a function in a class must be `self`. Additional parameters can be listed after `self`, and work exactly like parameters to a regular function.
```
class Human:
  def eat(self, food):
    print(self.name + " ate " + food)
    
bob = Human()
bob.name = "Bob"
bob.eat("pizza")
```

The `__init__` function can also take additional parameters. Conventionally, the parameters of the `__init__` function are values that the object is required to have. In the case of the `Human` class, every human must have a name, so it would be useful to add a `name` parameter to the `__init__` function.

```
class Human:
  def __init__(self, name):
    self.name = name
    print(name + " is born")

sally = Human("sally")
```

Problem: Vehicle

Define a `Vehicle` class with
- a `gas` attribute that stores how much fuel the vehicle has. This should initially be set to 0
- a constructor that takes a `mileage` parameter (in miles per gallon)
- a function `fill(gallons)`, which fills the given `gallons` of fuel in the vehicle
- a function `drive(miles)` which reduces the fuel by the amount required to drive the given number of `miles`

## Multiple classes

You can define multiple classes in the same program. An object's attribute can refer to another object, so 
- a hierarchy of information can be created

```
class Flower:
  def __init__(self):
    print("Flower blooms")
    self.seed = Seed()

class Seed:
  def __init__(self):
    print("Seed created")

flower = Flower()
```

Problem: Wizards and Wands

Create a `Wizard` class and a `Wand` class. 

The `Wand` has a
- constructor that takes a `name` parameter

The `Wizard` has a
- constructor that takes a `name` parameter, and creates a `Wand` object
- function `cast` that takes a string `spell` parameter, and prints the given `spell`


## Memory model

In the previous `Flower` and `Seed` example, we created a hierarchy of classes that can be represented by the diagram below.

[ object diagram for flower + seed ]

In larger programs, the hierarchy of objects will usually have several classes that refer to each other.

[ object diagram for something complex like a store ]

Given the memory diagram above, 
- we can write some code to interact with the program

```
store = Store()
store.name = "something"

a = Product("apples", 0.54)
b = Product("bananas", 0.93)

store.add_product(a, 10)
store.add_product(b, 10)

```

Problem: Bank
- given the memory model, write some code that performs a certain task. e.g.
- 
```
jp_morgan = Bank()

john = Customer("John Smith")
john_savings = Account(1842.15)
john_checking = Account(298.11)

john.add_account(johnSavings)
john.add_account(johnChecking)

jp_morgan.add_customer(john)
```
