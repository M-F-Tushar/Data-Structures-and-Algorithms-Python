# Object-Oriented Programming (OOP) Complete Guide (Easy Vocabulary)

This chapter explains OOP in simple words, with examples you can run in Python.
The goal is not to memorize definitions. The goal is to learn how to *design* code that is easier to read, reuse, and extend.

## Table of Contents
1. [Introduction to OOP](#1-introduction-to-object-oriented-programming)
2. [Core OOP Concepts](#2-core-oop-concepts)
3. [Python Implementation](#3-creating-classes-and-objects-in-python)
4. [Working with Attributes](#4-working-with-attributes)
5. [Working with Methods](#5-working-with-methods)
6. [Object Identification](#6-identifying-objects-in-programs)
7. [Practical Exercises](#7-exercises)
8. [Key Takeaways](#8-key-takeaways)
9. [Additional Notes](#9-additional-notes)

---

## 1. Introduction to Object-Oriented Programming

### 1.1 What is OOP and Why Use It?

**Object-Oriented Programming (OOP)** is a style of programming where you build your program using **objects**.
An object is like a small “package” that contains:

- **Data** (attributes)
- **Actions** (methods)

OOP helps when your program grows. It makes code easier to organize.

### 1.2 Why OOP is Useful

- **Build your own data structures**: later you will build linked lists, trees, graphs, etc.
- **Split work into parts**: different people can work on different classes.
- **Reuse code**: one class can be used in many projects.
- **Add features safely**: you can extend classes without rewriting everything.

### 1.3 Real-World Analogies

#### Smart Robot Project
```
Scenario: Building software for a smart robot
Parts: processor, touch sensors, speech recognition, movement

OOP Approach:
├── Processor Module (Team A)
├── Sensor Module (Team B)
├── Speech Module (Team C)
└── Movement Module (Team D)

Result: Each part is separate, but they work together.
```

#### Hotel Management System
```
Not OOP: One person does everything
├── Reception
├── Housekeeping
├── Cooking
└── Accounting

OOP: Different objects do different jobs
├── Receptionist Object: reserve_room(), check_in()
├── Housekeeper Object: clean_floor(), report_issue()
└── Manager Object: coordinates everyone

Result: Easier to scale and easier to maintain.
```

---

## 2. Core OOP Concepts

### 2.1 Class

A **class** is a blueprint.
It describes what an object will have (attributes) and what it can do (methods).

**Analogy**: A cookie cutter is the class. Cookies are objects made from it.

### 2.2 Object

An **object** is a real instance created from a class.

Important points:

- Every object has its own **identity** (it is a unique thing in memory).
- Every object has its own **state** (its current attribute values).
- Many objects can come from the same class.

### 2.3 Attribute

An **attribute** is data stored on an object.

Two common types:

- **Instance attributes**: belong to one object (usually created inside `__init__`).
- **Class attributes**: shared by all objects of the class.

### 2.4 Method

A **method** is a function that lives inside a class.
It usually reads or changes the object’s attributes.

---

### 2.5 Encapsulation (Keep Data + Rules Together)

**Encapsulation** means:

- keep the data and the rules for that data in the same place (the class)
- protect the object from “bad” changes

In Python, encapsulation is mostly done by *design*, not by strict access rules.

Example idea: a bank account should not allow negative deposits.

### 2.6 Abstraction (Hide Details)

**Abstraction** means you show only what users need.
You hide internal steps.

Example: you press “play” on your phone. You do not need to know every internal step.

In code: a method like `withdraw()` hides all the checks and updates inside it.

### 2.7 Inheritance (IS-A)

**Inheritance** means one class can reuse and extend another class.

- `Dog` IS-A `Animal`
- `Car` IS-A `Vehicle`

Use inheritance when it matches the real relationship.

### 2.8 Polymorphism (Same Method Name, Different Behavior)

**Polymorphism** means you can call the same method name on different objects, and each one does the right thing.

Example: many shapes can have an `area()` method.
Each shape calculates area differently.

### 2.9 Composition (HAS-A)

**Composition** means one object *contains* another object.

- A `Car` HAS-A `Engine`
- A `Playlist` HAS-A list of `Song`

Composition is often safer than inheritance for large systems.

### 2.10 Object Relationships (Association, Aggregation, Composition)

These words describe “how objects connect”:

- **Association**: objects know about each other (a `Student` knows a `Teacher`).
- **Aggregation**: a “whole-part” relation where parts can live without the whole (a `Team` has `Players`).
- **Composition**: a stronger “whole-part” relation where parts are owned by the whole (a `Car` owns its `Engine`).

---

## 3. Creating Classes and Objects in Python

### 3.1 Defining a Class

```python
class ClassName:
    pass
```

Naming style: **PascalCase** for class names (example: `StarCookie`).

Example:

```python
class StarCookie:
    pass
```

### 3.2 Creating Objects

```python
star_cookie_1 = StarCookie()
star_cookie_2 = StarCookie()

print(star_cookie_1)
print(star_cookie_2)
```

### 3.3 The `__init__` Method (Object Setup)

`__init__` runs when you create an object.
It is used to set the starting attributes.

```python
class StarCookie:
    def __init__(self, color, weight):
        self.color = color
        self.weight = weight

star_cookie = StarCookie("red", 15)
print(star_cookie.color)
print(star_cookie.weight)
```

### 3.4 What is `self`?

`self` is “this object”.
It lets the method read/change the attributes of the current object.

---

## 4. Working with Attributes

### 4.1 Instance Attributes

Instance attributes are stored per object.

```python
class StarCookie:
    def __init__(self, color, weight):
        self.color = color
        self.weight = weight

star_cookie_1 = StarCookie("red", 15)
star_cookie_2 = StarCookie("blue", 16)

print(star_cookie_1.color)   # red
print(star_cookie_2.color)   # blue
```

### 4.2 Default Attribute Values

Defaults make object creation easier.

```python
class YouTube:
    def __init__(self, username, subscribers=0):
        self.username = username
        self.subscribers = subscribers

user_1 = YouTube("Elshad")
user_2 = YouTube("Renat")

print(user_1.subscribers)  # 0
print(user_2.subscribers)  # 0
```

**⚠️ Pitfall: typos create new attributes**

Python lets you add new attributes at runtime.
This is flexible, but typos can hide bugs.

```python
user_2.subscriber = 5      # typo (subscriber vs subscribers)
print(user_2.subscribers)  # still 0
print(user_2.subscriber)   # 5
```

### 4.3 Class Attributes

Class attributes are shared.

```python
class StarCookie:
    milk = 0.1

    def __init__(self, color, weight):
        self.color = color
        self.weight = weight

star_cookie_1 = StarCookie("red", 15)
star_cookie_2 = StarCookie("blue", 16)

print(star_cookie_1.milk)  # 0.1
print(star_cookie_2.milk)  # 0.1
print(StarCookie.milk)     # 0.1
```

If you assign to `star_cookie_1.milk`, you create an **instance** attribute that overrides the class attribute for that object.

### 4.4 Inspecting Attributes with `__dict__`

```python
print(star_cookie_1.__dict__)
print(StarCookie.__dict__)
```

This is useful for debugging.

### 4.5 Encapsulation with Properties (`@property`)

Instead of letting users change an attribute directly, you can expose a safe “public” interface.

```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self._balance = balance  # '_' means "internal" by convention

    @property
    def balance(self):
        return self._balance

    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Deposit must be positive")
        self._balance += amount

account = BankAccount("Alice", 100)
print(account.balance)  # 100
account.deposit(50)
print(account.balance)  # 150
```

### 4.6 Attribute Visibility in Python (Public / _Protected / __Private)

Python uses naming conventions:

- `name` means “public”
- `_name` means “internal use”
- `__name` triggers name-mangling (harder to access by accident)

---

## 5. Working with Methods

### 5.1 Defining Instance Methods

```python
class Robot:
    def __init__(self, battery_level):
        self.battery_level = battery_level

    def enter_charge_mode(self):
        self.battery_level += 1

my_robot = Robot(50)
print(my_robot.battery_level)  # 50
my_robot.enter_charge_mode()
print(my_robot.battery_level)  # 51
```

### 5.2 Object Interaction (Objects Working Together)

```python
class YouTube:
    def __init__(self, username, subscribers=0, subscriptions=0):
        self.username = username
        self.subscribers = subscribers
        self.subscriptions = subscriptions

    def subscribe(self, user):
        user.subscribers += 1
        self.subscriptions += 1

user_1 = YouTube("Elshad")
user_2 = YouTube("Renat")

user_1.subscribe(user_2)
print(user_1.subscriptions)  # 1
print(user_2.subscribers)    # 1
```

### 5.3 Class Methods and Static Methods

Sometimes a method belongs to the class, not to one object.

```python
class Temperature:
    def __init__(self, celsius):
        self.celsius = celsius

    @classmethod
    def from_fahrenheit(cls, fahrenheit):
        c = (fahrenheit - 32) * 5 / 9
        return cls(c)

    @staticmethod
    def is_freezing(celsius):
        return celsius <= 0

t = Temperature.from_fahrenheit(212)
print(t.celsius)                 # 100.0
print(Temperature.is_freezing(0))  # True
```

### 5.4 Inheritance and `super()`

```python
class Vehicle:
    def __init__(self, brand):
        self.brand = brand

    def move(self):
        return "Moving"


class Car(Vehicle):
    def __init__(self, brand, doors):
        super().__init__(brand)
        self.doors = doors

    def move(self):
        return "Driving"


car = Car("Toyota", 4)
print(car.brand)  # Toyota
print(car.move()) # Driving
```

### 5.5 Polymorphism Example

```python
class Circle:
    def __init__(self, r):
        self.r = r

    def area(self):
        return 3.14159 * self.r * self.r


class Rectangle:
    def __init__(self, w, h):
        self.w = w
        self.h = h

    def area(self):
        return self.w * self.h


shapes = [Circle(2), Rectangle(3, 4)]
for s in shapes:
    print(s.area())
```

Both objects support `.area()`. That is polymorphism.

### 5.6 Composition Example

```python
class Engine:
    def start(self):
        return "Engine started"


class Car:
    def __init__(self, brand):
        self.brand = brand
        self.engine = Engine()

    def start(self):
        return self.engine.start()


car = Car("Honda")
print(car.start())
```

### 5.7 Special Methods ("Dunder" Methods)

Python uses special method names like `__str__`.
They let your objects work nicely with built-in functions.

```python
class StarCookie:
    def __init__(self, color, weight):
        self.color = color
        self.weight = weight

    def __str__(self):
        return f"StarCookie(color={self.color}, weight={self.weight})"


cookie = StarCookie("red", 15)
print(cookie)
```

Common ones:

- `__init__` (setup)
- `__str__` (nice text)
- `__repr__` (developer-friendly text)
- `__len__` (length)
- `__eq__` (equality)

---

## 6. Identifying Objects in Programs

### 6.1 What Qualifies as an Object?

An object is something that has:

- **Identity**: it exists as a unique thing
- **State**: it stores data
- **Behavior**: it can do actions

### 6.2 Identity vs Equality

- `is` checks if two names point to the **same object**.
- `==` checks if two objects are **equal in value** (depends on `__eq__`).

```python
a = [1, 2]
b = [1, 2]

print(a == b)  # True
print(a is b)  # False
```

### 6.3 Helpful Tools: `id`, `type`, `isinstance`

```python
print(id(a))
print(type(a))
print(isinstance(a, list))
```

### 6.4 Examples of Objects

#### Tangible Objects
| Object | Attributes | Behaviors |
|--------|------------|-----------|
| Mug | color, size, fill_level | (often none) |
| Cookie | color, weight | decorate(), consume() |
| Cell Phone | color, battery_level | ring(), text(), play_music() |

#### Non-Tangible Objects
| Object | Attributes | Behaviors |
|--------|------------|-----------|
| Bank Account | account_number, balance | deposit(), withdraw() |
| Event | date, location | schedule(), cancel() |

### 6.5 Quick Design Guide

- **Nouns** become classes/objects (Car, Student, Account)
- **Verbs** become methods (drive, enroll, deposit)

---

## 7. Exercises

### Exercise 1: Simple Class and Objects

Task: Create a `Car` class with `model` and `speed`.

```python
class Car:
    def __init__(self, model, speed):
        self.model = model
        self.speed = speed

car_1 = Car("Toyota", 120)
car_2 = Car("Honda", 150)

print(f"{car_1.model} speed: {car_1.speed}")
print(f"{car_2.model} speed: {car_2.speed}")
```

### Exercise 2: Class Attributes

Task: Add `fuel_type` as a class attribute.

```python
class Car:
    fuel_type = "Petrol"

    def __init__(self, model, speed):
        self.model = model
        self.speed = speed

car_1 = Car("Toyota", 120)
car_2 = Car("Honda", 150)

print(car_1.fuel_type)
print(car_2.fuel_type)
print(Car.fuel_type)

car_1.fuel_type = "Diesel"
print(car_1.fuel_type)
print(car_2.fuel_type)
```

### Exercise 3: Adding Methods

Task: Add an `accelerate` method that increases speed by 10.

```python
class Car:
    def __init__(self, model, speed):
        self.model = model
        self.speed = speed

    def accelerate(self):
        self.speed += 10

car_1 = Car("Toyota", 120)
print(car_1.speed)
car_1.accelerate()
print(car_1.speed)
```

### Exercise 4: Object Interaction

Task: Create a `Student` class with a `make_friend` method.

```python
class Student:
    def __init__(self, name, friends=0):
        self.name = name
        self.friends = friends

    def make_friend(self, other_student):
        self.friends += 1
        other_student.friends += 1

student_1 = Student("Alice")
student_2 = Student("Bob")

student_1.make_friend(student_2)
print(student_1.friends)
print(student_2.friends)
```

### Exercise 5: Inheritance

Task: Create `Animal` and `Dog`. Dog should reuse Animal and add a method.

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return "..."


class Dog(Animal):
    def speak(self):
        return "Woof"


dog = Dog("Buddy")
print(dog.name)
print(dog.speak())
```

### Exercise 6: Encapsulation with a Property

Task: Create a `BankAccount` where balance cannot go below 0.

Hint: use `_balance`, `@property`, and a `withdraw()` method.

---

## 8. Key Takeaways

- OOP organizes code into **classes** (blueprints) and **objects** (instances).
- Objects have **attributes** (data) and **methods** (actions).
- The “big 4” ideas are: **encapsulation**, **abstraction**, **inheritance**, **polymorphism**.
- **Composition** (HAS-A) is often a great alternative to inheritance (IS-A).
- Python supports OOP deeply, but it also trusts you: good naming and good design matter.

---

## 9. Additional Notes

### 9.1 When to Use OOP (and When Not To)

OOP is useful when you have:

- many related pieces of data and behavior
- clear “things” in your problem (accounts, users, nodes, lists)
- code that needs to grow over time

You might *not* need heavy OOP for small scripts or simple one-time tasks.

### 9.2 Common Pitfalls (Beginner Friendly)

- Typos create new attributes (bug hiding).
- Using class attributes for per-object data.
- Forgetting `self` in method definitions.
- Choosing inheritance when composition fits better.

### 9.3 Quick SOLID Overview (Very Simple)

- **S (Single responsibility)**: one class = one main job.
- **O (Open/closed)**: add features by extending, not rewriting.
- **L (Liskov substitution)**: child class should behave like parent where expected.
- **I (Interface segregation)**: don’t force classes to implement unused methods.
- **D (Dependency inversion)**: depend on abstractions, not concrete details.

### 9.4 Advanced Python OOP Topics to Learn Next

- `dataclasses` for simple “data objects”
- abstract base classes (`abc`) for stricter abstraction
- `__slots__` to reduce memory and prevent typos
- type hints for clarity (helps readers and tools)

This guide is meant to be practical: try the examples, then do the exercises.
