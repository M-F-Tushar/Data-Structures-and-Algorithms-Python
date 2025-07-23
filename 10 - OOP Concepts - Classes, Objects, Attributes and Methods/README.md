# Object-Oriented Programming (OOP) Complete Guide

## Table of Contents
1. [Introduction to OOP](#1-introduction-to-object-oriented-programming)
2. [Core OOP Concepts](#2-core-oop-concepts)
3. [Python Implementation](#3-creating-classes-and-objects-in-python)
4. [Working with Attributes](#4-working-with-attributes)
5. [Working with Methods](#5-working-with-methods)
6. [Object Identification](#6-identifying-objects-in-programs)
7. [Practical Exercises](#7-exercises)
8. [Key Takeaways](#8-key-takeaways)

---

## 1. Introduction to Object-Oriented Programming

### 1.1 What is OOP and Why Use It?

**Object-Oriented Programming (OOP)** is a programming paradigm that organizes code into objects, which are instances of classes. OOP models real-world entities, making it easier to manage complex software projects by breaking them into modular, reusable components.

### 1.2 Why OOP is Essential

- **Transition from Built-in to Custom Data Structures**: Move from Python's built-in structures to creating custom ones (e.g., linked lists)
- **Modular Design**: Teams can work on separate components simultaneously
- **Code Reusability**: Modules can be reused across different projects
- **Scalability**: Easier to manage and extend large projects

### 1.3 Real-World Analogies

#### Smart Robot Project
```
Scenario: Building software for a smart robot
Components: processor, touch sensors, speech recognition, degrees of freedom

OOP Approach:
├── Processor Module (Team A)
├── Sensor Module (Team B)
├── Speech Module (Team C)
└── Movement Module (Team D)

Benefits: Modularity, Reusability, Scalability
```

#### Hotel Management System
```
Traditional Approach: One person handles all roles
├── Reception
├── Housekeeping
├── Cooking
└── Accounting
❌ Inefficient and error-prone

OOP Approach: Specialized roles (objects)
├── Receptionist Object
│   ├── Attributes: name, shift
│   └── Methods: reserve_room(), check_in()
├── Housekeeper Object
│   ├── Attributes: responsible_floors, is_cleaning
│   └── Methods: clean_floor(), notify_supervisor()
└── Manager Object (oversees all objects)
✅ Efficient, scalable, maintainable
```

---

## 2. Core OOP Concepts

### 2.1 Class
**Definition**: A blueprint or template that defines the structure and behavior of objects.

**Analogy**: Cookie cutter (class) defines the shape of cookies (objects) but is not a cookie itself.

**Components**:
- **Name**: Identifies the class (e.g., `StarCookie`)
- **Attributes**: Variables describing properties (e.g., `weight`, `color`)
- **Methods**: Functions defining behaviors (e.g., `decorate()`, `consume()`)

### 2.2 Object
**Definition**: An instance of a class, created based on the class's blueprint.

**Key Properties**:
- **Unique Identity**: Each object exists independently
- **Individual State**: Can have different attribute values
- **Shared Structure**: All objects from same class share the same blueprint

**Analogy**: Cookies cut from the same star-shaped cutter are objects. Each can have different colors or weights but shares the same shape.

### 2.3 Attribute
**Definition**: A variable associated with an object, representing its properties or state.

**Types**:
- **Instance Attributes**: Unique to each object
- **Class Attributes**: Shared across all objects of a class

### 2.4 Method
**Definition**: A function defined within a class that describes behaviors or actions an object can perform.

**Key Difference**: Methods are associated with objects, while functions are standalone.

---

## 3. Creating Classes and Objects in Python

### 3.1 Defining a Class

**Syntax**:
```python
class ClassName:
    pass  # Placeholder for empty class
```

**Naming Convention**: PascalCase (e.g., `StarCookie`, `SmartRobot`)

**Example**:
```python
class StarCookie:
    pass
```

### 3.2 Creating Objects

**Syntax**:
```python
object_name = ClassName()
```

**Example**:
```python
star_cookie_1 = StarCookie()
star_cookie_2 = StarCookie()

print(star_cookie_1)  # <StarCookie object at 0x...>
print(star_cookie_2)  # <StarCookie object at 0x...>
```

---

## 4. Working with Attributes

### 4.1 Instance Attributes

**Definition**: Unique to each object, initialized using the `__init__` method.

**Syntax**:
```python
class ClassName:
    def __init__(self, param1, param2):
        self.param1 = param1
        self.param2 = param2
```

**Example**: StarCookie Class
```python
class StarCookie:
    def __init__(self, color, weight):
        self.color = color
        self.weight = weight

# Create objects
star_cookie_1 = StarCookie("red", 15)
star_cookie_2 = StarCookie("blue", 16)

# Access attributes
print(star_cookie_1.color)   # Output: red
print(star_cookie_1.weight)  # Output: 15
print(star_cookie_2.color)   # Output: blue
print(star_cookie_2.weight)  # Output: 16
```

### 4.2 Default Attribute Values

**Example**: YouTube User Class
```python
class YouTube:
    def __init__(self, username, subscribers=0):
        self.username = username
        self.subscribers = subscribers

# Create objects
user_1 = YouTube("Elshad")
user_2 = YouTube("Renat")

print(f"{user_1.username} subscribers: {user_1.subscribers}")  # Elshad subscribers: 0
print(f"{user_2.username} subscribers: {user_2.subscribers}")  # Renat subscribers: 0

# Modify attribute
user_2.subscribers = 5
print(f"{user_2.username} subscribers: {user_2.subscribers}")  # Renat subscribers: 5
```

**⚠️ Pitfall: Typos Create New Attributes**
```python
user_2.subscriber = 5  # Typo: creates new attribute
print(user_2.subscribers)  # Output: 0 (original unchanged)
print(user_2.subscriber)   # Output: 5 (new attribute)
```

### 4.3 Class Attributes

**Definition**: Shared across all instances of a class.

**Example**:
```python
class StarCookie:
    milk = 0.1  # Class attribute (liters of milk per cookie)

    def __init__(self, color, weight):
        self.color = color
        self.weight = weight

# Create objects
star_cookie_1 = StarCookie("red", 15)
star_cookie_2 = StarCookie("blue", 16)

# Access class attribute
print(star_cookie_1.milk)  # Output: 0.1
print(star_cookie_2.milk)  # Output: 0.1
print(StarCookie.milk)     # Output: 0.1
```

**Modifying Class Attributes**:
```python
# Modify for specific object (creates instance attribute)
star_cookie_1.milk = 0.2
print(star_cookie_1.milk)  # Output: 0.2
print(star_cookie_2.milk)  # Output: 0.1
print(StarCookie.milk)     # Output: 0.1

# Modify for all objects
StarCookie.milk = 0.3
print(star_cookie_1.milk)  # Output: 0.2 (instance overrides)
print(star_cookie_2.milk)  # Output: 0.3 (uses class attribute)
print(StarCookie.milk)     # Output: 0.3
```

**Inspecting Attributes with `__dict__`**:
```python
print(star_cookie_1.__dict__)  # {'color': 'red', 'weight': 15, 'milk': 0.2}
print(star_cookie_2.__dict__)  # {'color': 'blue', 'weight': 16}
print(StarCookie.__dict__)     # {..., 'milk': 0.3, ...}
```

---

## 5. Working with Methods

### 5.1 Defining Methods

**Syntax**:
```python
class ClassName:
    def method_name(self, param1, param2):
        # Method logic
        self.attribute = param1  # Access or modify attributes
```

### 5.2 Example: Robot Class

```python
class Robot:
    def __init__(self, battery_level):
        self.battery_level = battery_level

    def enter_charge_mode(self):
        self.battery_level += 1

# Usage
my_robot = Robot(50)
print(my_robot.battery_level)  # Output: 50
my_robot.enter_charge_mode()
print(my_robot.battery_level)  # Output: 51
```

### 5.3 Example: Object Interaction

```python
class YouTube:
    def __init__(self, username, subscribers=0, subscriptions=0):
        self.username = username
        self.subscribers = subscribers
        self.subscriptions = subscriptions

    def subscribe(self, user):
        user.subscribers += 1      # Increase other user's subscribers
        self.subscriptions += 1    # Increase this user's subscriptions

# Create objects
user_1 = YouTube("Elshad")
user_2 = YouTube("Renat")

# User 1 subscribes to User 2
user_1.subscribe(user_2)
print(f"{user_1.username} subscribers: {user_1.subscribers}, subscriptions: {user_1.subscriptions}")
# Output: Elshad subscribers: 0, subscriptions: 1
print(f"{user_2.username} subscribers: {user_2.subscribers}, subscriptions: {user_2.subscriptions}")
# Output: Renat subscribers: 1, subscriptions: 0
```

---

## 6. Identifying Objects in Programs

### 6.1 What Qualifies as an Object?

Objects represent entities with:
- **Identity**: Unique existence
- **Attributes**: Properties describing state
- **Behaviors**: Actions they can perform

### 6.2 Examples

#### Tangible Objects
| Object | Attributes | Behaviors |
|--------|------------|-----------|
| Mug | color, size, fill_level | (none typically) |
| Cookie | color, weight | decorate(), consume() |
| Cell Phone | color, battery_level | ring(), text(), play_music() |

#### Non-Tangible Objects
| Object | Attributes | Behaviors |
|--------|------------|-----------|
| Bank Account | account_number, balance | deposit(), withdraw() |
| Event | date, location | schedule(), cancel() |

### 6.3 Design Guidelines

- **Nouns** → Objects (e.g., mug, event)
- **Verbs** → Methods/Behaviors (e.g., texting, ringing)

---

## 7. Exercises

### Exercise 1: Simple Class and Objects

**Task**: Create a `Car` class with `model` and `speed` attributes.

```python
class Car:
    def __init__(self, model, speed):
        self.model = model
        self.speed = speed

# Create objects
car_1 = Car("Toyota", 120)
car_2 = Car("Honda", 150)

# Print attributes
print(f"{car_1.model} speed: {car_1.speed}")  # Toyota speed: 120
print(f"{car_2.model} speed: {car_2.speed}")  # Honda speed: 150
```

### Exercise 2: Class Attributes

**Task**: Add `fuel_type` as a class attribute.

```python
class Car:
    fuel_type = "Petrol"  # Class attribute

    def __init__(self, model, speed):
        self.model = model
        self.speed = speed

# Create objects
car_1 = Car("Toyota", 120)
car_2 = Car("Honda", 150)

# Print class attribute
print(car_1.fuel_type)    # Petrol
print(car_2.fuel_type)    # Petrol
print(Car.fuel_type)      # Petrol

# Modify class attribute for one object
car_1.fuel_type = "Diesel"
print(car_1.fuel_type)    # Diesel
print(car_2.fuel_type)    # Petrol
```

### Exercise 3: Adding Methods

**Task**: Add an `accelerate` method that increases speed by 10.

```python
class Car:
    def __init__(self, model, speed):
        self.model = model
        self.speed = speed

    def accelerate(self):
        self.speed += 10

# Usage
car_1 = Car("Toyota", 120)
print(f"Initial speed: {car_1.speed}")  # Initial speed: 120
car_1.accelerate()
print(f"Speed after acceleration: {car_1.speed}")  # Speed after acceleration: 130
```

### Exercise 4: Object Interaction

**Task**: Create a `Student` class with a `make_friend` method.

```python
class Student:
    def __init__(self, name, friends=0):
        self.name = name
        self.friends = friends

    def make_friend(self, other_student):
        self.friends += 1
        other_student.friends += 1

# Create objects
student_1 = Student("Alice")
student_2 = Student("Bob")

# Make friends
student_1.make_friend(student_2)
print(f"{student_1.name} friends: {student_1.friends}")  # Alice friends: 1
print(f"{student_2.name} friends: {student_2.friends}")  # Bob friends: 1
```

---

## 8. Key Takeaways

### 8.1 Core Concepts
- **Classes**: Blueprints defining structure and behavior
- **Objects**: Instances with unique identities and attributes
- **Attributes**: Instance (unique) vs Class (shared) attributes
- **Methods**: Functions tied to objects using `self`

### 8.2 Python Implementation Best Practices
- Use `class` keyword with PascalCase naming
- Initialize attributes with `__init__` method
- Set default values for optional parameters
- Access attributes/methods with dot notation
- Be cautious of dynamic attribute creation (typos)

### 8.3 Design Principles
- **Modularity**: Break complex systems into manageable objects
- **Reusability**: Design objects for use across projects
- **Real-world Modeling**: Model both tangible and abstract entities
- **Clarity**: Focus on nouns (objects) and verbs (methods)

### 8.4 Debugging Tools
- Use `__dict__` to inspect object/class attributes
- Understand namespace differences between instance and class attributes
- Follow Python naming conventions consistently

---

## 9. Additional Notes

### 9.1 Advanced Considerations
- **Predefined Classes**: Python provides built-in classes (strings, lists, etc.)
- **Dynamic Attributes**: Python allows runtime attribute creation (use with caution)
- **Attribute Restriction**: Advanced techniques like `__slots__` can prevent dynamic attributes

### 9.2 Common Pitfalls
- Typos creating unintended attributes
- Confusion between instance and class attributes
- Forgetting `self` parameter in method definitions
- Improper use of class attributes for instance-specific data

This comprehensive guide provides a structured foundation for understanding and implementing Object-Oriented Programming concepts in Python.
