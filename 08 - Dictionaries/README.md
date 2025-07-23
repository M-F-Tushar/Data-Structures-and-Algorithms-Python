# Complete Python Dictionary Tutorial

## Table of Contents
1. [What is a Dictionary?](#what-is-a-dictionary)
2. [Creating Dictionaries](#creating-dictionaries)
3. [How Dictionaries Work in Memory](#how-dictionaries-work-in-memory)
4. [Basic Operations](#basic-operations)
5. [Dictionary Methods](#dictionary-methods)
6. [Advanced Features](#advanced-features)
7. [Performance Analysis](#performance-analysis)
8. [Dictionary vs Other Data Structures](#dictionary-vs-other-data-structures)
9. [Best Practices](#best-practices)
10. [Practical Exercises](#practical-exercises)

---

## 1. What is a Dictionary?

A dictionary is Python's built-in **associative array** - an unordered, mutable collection that stores data as key-value pairs. Think of it as a real-world dictionary where you look up definitions (values) using words (keys).

### Key Characteristics
- **Unordered**: Elements aren't stored in insertion order (Python 3.7+ maintains insertion order as implementation detail)
- **Mutable**: Can be modified after creation
- **Indexed by keys**: Access elements using unique keys instead of numeric indices
- **Keys must be**: Unique and immutable (strings, numbers, tuples, frozensets)
- **Values can be**: Any data type including other dictionaries (nested)

### Real-World Analogy
```
Library Card Catalog System:
├── Key: Book Title → Value: Location/Details
├── Key: "Python Programming" → Value: "Section A, Shelf 5"
└── Key: "Data Structures" → Value: "Section B, Shelf 2"
```

### Basic Example
```python
student_grades = {
    "Alice": 95,
    "Bob": 87,
    "Charlie": 92,
    "Diana": 98
}

# Access: O(1) average time complexity
print(student_grades["Alice"])  # Output: 95
```

---

## 2. Creating Dictionaries

### Method 1: Empty Dictionary
```python
# Using dict() constructor
empty_dict1 = dict()

# Using curly braces (more Pythonic)
empty_dict2 = {}

# Both create: {}
```

### Method 2: Dictionary with Initial Data
```python
# Direct key-value assignment
colors = {
    "red": "#FF0000",
    "green": "#00FF00",
    "blue": "#0000FF"
}

# Using dict() with keyword arguments
colors = dict(red="#FF0000", green="#00FF00", blue="#0000FF")

# From list of tuples
color_pairs = [("red", "#FF0000"), ("green", "#00FF00")]
colors = dict(color_pairs)

# From zip (combining two lists)
names = ["red", "green", "blue"]
hex_codes = ["#FF0000", "#00FF00", "#0000FF"]
colors = dict(zip(names, hex_codes))
```

### Method 3: Dictionary Comprehension
```python
# Create squares dictionary
squares = {x: x**2 for x in range(1, 6)}
# Result: {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# With conditional logic
even_squares = {x: x**2 for x in range(10) if x % 2 == 0}
# Result: {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}
```

**Time Complexity**: O(1) for empty dict, O(n) for n elements

---

## 3. How Dictionaries Work in Memory

Dictionaries use **hash tables** for efficient operations:

```
Hash Table Structure:
┌─────────────────────────────────────┐
│ Key → Hash Function → Index → Value │
├─────────────────────────────────────┤
│ "name" → hash("name") → 3 → "Alice" │
│ "age" → hash("age") → 7 → 25        │
│ "city" → hash("city") → 1 → "NYC"   │
└─────────────────────────────────────┘
```

### Hash Collision Handling
When different keys produce the same hash (collision), Python uses:
- **Open addressing** with probing
- **Separate chaining** for overflow

### Memory Optimization (Python 3.6+)
- **Compact representation**: Keys and values stored separately
- **Insertion order preserved** as implementation detail
- **25% less memory usage** compared to older versions

---

## 4. Basic Operations

### Insertion and Updates
```python
student = {"name": "John", "age": 20}

# Add new key-value pair
student["major"] = "Computer Science"

# Update existing value
student["age"] = 21

# Multiple updates
student.update({"gpa": 3.8, "year": "Junior"})

print(student)
# {'name': 'John', 'age': 21, 'major': 'Computer Science', 'gpa': 3.8, 'year': 'Junior'}
```

### Accessing Elements
```python
# Direct access (raises KeyError if key doesn't exist)
name = student["name"]

# Safe access with default value
height = student.get("height", "Not specified")
gpa = student.get("gpa", 0.0)

# Check if key exists before accessing
if "email" in student:
    email = student["email"]
else:
    email = "No email provided"
```

### Traversing Dictionaries
```python
student = {"name": "Alice", "age": 22, "major": "Physics"}

# Method 1: Iterate over keys
for key in student:
    print(f"{key}: {student[key]}")

# Method 2: Iterate over key-value pairs (more efficient)
for key, value in student.items():
    print(f"{key}: {value}")

# Method 3: Iterate over values only
for value in student.values():
    print(value)

# Method 4: With enumeration
for index, (key, value) in enumerate(student.items()):
    print(f"{index}: {key} = {value}")
```

### Searching Elements
```python
# Search by key (O(1) - efficient)
def has_key(dictionary, key):
    return key in dictionary

# Search by value (O(n) - linear search)
def find_key_by_value(dictionary, target_value):
    for key, value in dictionary.items():
        if value == target_value:
            return key
    return None

# Multiple value search
def find_keys_by_value(dictionary, target_value):
    return [key for key, value in dictionary.items() if value == target_value]

# Example usage
student = {"name": "Bob", "age": 20, "grade": "A", "score": 95}
print(has_key(student, "name"))  # True
print(find_key_by_value(student, 20))  # age
```

### Deleting Elements
```python
student = {"name": "Charlie", "age": 19, "major": "Math", "gpa": 3.5}

# Method 1: del statement
del student["gpa"]  # Removes key-value pair completely

# Method 2: pop() - returns value before deletion
age = student.pop("age")  # Returns 19
major = student.pop("major", "Unknown")  # With default value

# Method 3: popitem() - removes and returns last inserted item (Python 3.7+)
last_item = student.popitem()  # Returns ("name", "Charlie")

# Method 4: clear() - removes all elements
student.clear()  # Results in {}

# Method 5: Conditional deletion
grades = {"Alice": 95, "Bob": 67, "Charlie": 89, "Diana": 45}
# Remove failing grades (< 70)
failing_students = [name for name, grade in grades.items() if grade < 70]
for name in failing_students:
    del grades[name]
```

---

## 5. Dictionary Methods

### Essential Methods Reference

| Method | Description | Example | Return Type |
|--------|-------------|---------|-------------|
| `keys()` | Get all keys | `dict.keys()` | dict_keys |
| `values()` | Get all values | `dict.values()` | dict_values |
| `items()` | Get key-value pairs | `dict.items()` | dict_items |
| `get(key, default)` | Safe value retrieval | `dict.get('name', 'Unknown')` | Any |
| `setdefault(key, default)` | Get or set default | `dict.setdefault('count', 0)` | Any |
| `update(other)` | Merge dictionaries | `dict.update({'new': 'value'})` | None |
| `copy()` | Shallow copy | `dict.copy()` | dict |
| `fromkeys(seq, value)` | Create from sequence | `dict.fromkeys(['a','b'], 0)` | dict |

### Detailed Method Examples
```python
student = {"name": "Emma", "age": 21, "major": "Biology"}

# keys(), values(), items() - return view objects (dynamic)
keys = student.keys()    # dict_keys(['name', 'age', 'major'])
values = student.values()  # dict_values(['Emma', 21, 'Biology'])
items = student.items()  # dict_items([('name', 'Emma'), ('age', 21), ('major', 'Biology')])

# Convert views to lists if needed
key_list = list(student.keys())
value_list = list(student.values())

# setdefault() - useful for counters and nested structures
grades = {}
grades.setdefault("Alice", []).append(95)  # Creates list if key doesn't exist
grades.setdefault("Alice", []).append(87)  # Appends to existing list
# Result: {"Alice": [95, 87]}

# update() - multiple ways to merge
base_config = {"timeout": 30, "retries": 3}
user_config = {"timeout": 60, "debug": True}

base_config.update(user_config)  # Merges user_config into base_config
# Alternative update methods:
# base_config.update([("new_key", "new_value")])
# base_config.update(extra_option="value")

# fromkeys() - create dictionary with same value for multiple keys
default_scores = dict.fromkeys(["Alice", "Bob", "Charlie"], 0)
# Result: {"Alice": 0, "Bob": 0, "Charlie": 0}

# Be careful with mutable default values!
# Wrong way:
wrong_dict = dict.fromkeys(["a", "b"], [])  # All keys share same list!
# Right way:
right_dict = {key: [] for key in ["a", "b"]}  # Each key gets its own list
```

---

## 6. Advanced Features

### Dictionary Comprehensions
```python
# Basic syntax: {key_expr: value_expr for item in iterable}

# Example 1: Word lengths
words = ["apple", "banana", "cherry", "date"]
word_lengths = {word: len(word) for word in words}
# Result: {'apple': 5, 'banana': 6, 'cherry': 6, 'date': 4}

# Example 2: Conditional comprehension
numbers = range(1, 11)
even_squares = {n: n**2 for n in numbers if n % 2 == 0}
# Result: {2: 4, 4: 16, 6: 36, 8: 64, 10: 100}

# Example 3: Nested comprehension
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flattened = {f"pos_{i}_{j}": matrix[i][j] 
            for i in range(len(matrix)) 
            for j in range(len(matrix[i]))}

# Example 4: Transform existing dictionary
original_prices = {"apple": 1.20, "banana": 0.50, "orange": 0.80}
# Apply 10% discount
discounted = {item: price * 0.9 for item, price in original_prices.items()}
```

### Nested Dictionaries
```python
# Student database with nested structure
students = {
    "001": {
        "name": "Alice Johnson",
        "grades": {"math": 95, "science": 92, "english": 88},
        "contact": {"email": "alice@email.com", "phone": "123-456-7890"}
    },
    "002": {
        "name": "Bob Smith",
        "grades": {"math": 87, "science": 91, "english": 94},
        "contact": {"email": "bob@email.com", "phone": "098-765-4321"}
    }
}

# Accessing nested data
alice_math_grade = students["001"]["grades"]["math"]  # 95
bob_email = students["002"]["contact"]["email"]  # bob@email.com

# Safe nested access with get()
alice_phone = students.get("001", {}).get("contact", {}).get("phone", "N/A")

# Adding to nested dictionary
students["001"]["grades"]["history"] = 90
students["003"] = {
    "name": "Charlie Brown",
    "grades": {},
    "contact": {}
}
```

### Merging Dictionaries (Python 3.9+)
```python
# Method 1: Union operator (|) - Python 3.9+
dict1 = {"a": 1, "b": 2}
dict2 = {"c": 3, "d": 4}
merged = dict1 | dict2  # {'a': 1, 'b': 2, 'c': 3, 'd': 4}

# Method 2: Update operator (|=)
dict1 |= dict2  # Modifies dict1 in place

# Method 3: Dictionary unpacking (Python 3.5+)
merged = {**dict1, **dict2}

# Method 4: Traditional update()
result = dict1.copy()
result.update(dict2)
```

---

## 7. Performance Analysis

### Time Complexity Summary
| Operation | Average Case | Worst Case | Notes |
|-----------|-------------|------------|-------|
| Access (`dict[key]`) | O(1) | O(n) | Hash collision dependent |
| Insertion (`dict[key] = value`) | O(1) | O(n) | May trigger resize |
| Deletion (`del dict[key]`) | O(1) | O(n) | Hash collision dependent |
| Search by key (`key in dict`) | O(1) | O(n) | Most efficient search |
| Search by value | O(n) | O(n) | Must scan all values |
| Iteration | O(n) | O(n) | Visit each key-value pair |
| `len(dict)` | O(1) | O(1) | Counter maintained |

### Space Complexity
- **Base overhead**: ~240 bytes (empty dictionary)
- **Per entry**: ~24 bytes + key size + value size
- **Load factor**: Maintained at ~2/3 for performance

### Performance Tips
```python
# Efficient: Use 'in' for key checking
if "key" in my_dict:
    value = my_dict["key"]

# Less efficient: Using try/except for existing keys
try:
    value = my_dict["key"]
except KeyError:
    value = None

# Efficient: Use get() with default
value = my_dict.get("key", default_value)

# Efficient: Use items() for key-value iteration
for key, value in my_dict.items():
    process(key, value)

# Less efficient: Access value via key in loop
for key in my_dict:
    value = my_dict[key]  # Extra hash lookup
    process(key, value)
```

---

## 8. Dictionary vs Other Data Structures

### Dictionary vs List
| Feature | Dictionary | List |
|---------|------------|------|
| **Ordering** | Insertion order (3.7+) | Index-based ordering |
| **Access Method** | By key | By index |
| **Access Time** | O(1) average | O(1) |
| **Search Time** | O(1) by key, O(n) by value | O(n) |
| **Memory Usage** | Higher overhead | Lower overhead |
| **Use Case** | Key-value mappings | Sequential data |

### Dictionary vs Set
| Feature | Dictionary | Set |
|---------|------------|-----|
| **Data Storage** | Key-value pairs | Unique values only |
| **Access Method** | `dict[key]` | `value in set` |
| **Modification** | `dict[key] = value` | `set.add(value)` |
| **Use Case** | Mappings, caching | Membership testing, deduplication |

### When to Use Dictionaries
- **Lookup tables**: Fast data retrieval by identifier
- **Caching**: Store computed results
- **Counting**: Frequency analysis
- **Grouping**: Organize data by categories
- **Configuration**: Settings and parameters
- **Database records**: Structured data representation

---

## 9. Best Practices

### Naming Conventions
```python
# Good: Descriptive key names
user_profile = {
    "user_id": 12345,
    "username": "alice_johnson",
    "email": "alice@example.com",
    "created_at": "2024-01-15"
}

# Avoid: Generic or ambiguous keys
data = {
    "id": 12345,
    "name": "alice_johnson",
    "contact": "alice@example.com",
    "date": "2024-01-15"
}
```

### Error Handling
```python
# Safe key access patterns
def get_user_email(user_dict, user_id):
    # Pattern 1: Using get() with default
    user = user_dict.get(user_id, {})
    return user.get("email", "No email provided")
    
    # Pattern 2: Using in operator
    if user_id in user_dict and "email" in user_dict[user_id]:
        return user_dict[user_id]["email"]
    return "No email provided"
    
    # Pattern 3: Try/except for exceptional cases
    try:
        return user_dict[user_id]["email"]
    except KeyError:
        return "No email provided"
```

### Memory Management
```python
# Use slots for memory-efficient classes
class Student:
    __slots__ = ['name', 'age', 'grades']
    
    def __init__(self, name, age):
        self.name = name
        self.age = age
        self.grades = {}

# Clear references when done
large_dict = {i: f"value_{i}" for i in range(1000000)}
# ... use dictionary ...
large_dict.clear()  # Free memory
large_dict = None   # Remove reference
```

### Common Patterns
```python
# Pattern 1: Default dictionary behavior
from collections import defaultdict

# Instead of:
word_count = {}
for word in words:
    if word in word_count:
        word_count[word] += 1
    else:
        word_count[word] = 1

# Use:
word_count = defaultdict(int)
for word in words:
    word_count[word] += 1

# Pattern 2: Grouping data
from itertools import groupby

students = [
    {"name": "Alice", "grade": "A", "subject": "Math"},
    {"name": "Bob", "grade": "B", "subject": "Math"},
    {"name": "Charlie", "grade": "A", "subject": "Science"}
]

# Group by grade
by_grade = defaultdict(list)
for student in students:
    by_grade[student["grade"]].append(student)

# Pattern 3: Configuration merging
def merge_configs(default_config, user_config):
    """Merge user config into default config."""
    merged = default_config.copy()
    merged.update(user_config)
    return merged

default = {"timeout": 30, "retries": 3, "debug": False}
user = {"timeout": 60, "debug": True}
final_config = merge_configs(default, user)
```

---

## 10. Practical Exercises

### Exercise 1: Word Frequency Counter
```python
def count_word_frequency(text):
    """Count frequency of each word in text."""
    words = text.lower().split()
    frequency = {}
    
    for word in words:
        # Remove punctuation
        word = word.strip(".,!?;:")
        frequency[word] = frequency.get(word, 0) + 1
    
    return frequency

# Test
text = "The quick brown fox jumps over the lazy dog. The dog was lazy."
result = count_word_frequency(text)
print(result)
# {'the': 3, 'quick': 1, 'brown': 1, 'fox': 1, 'jumps': 1, 'over': 1, 'lazy': 2, 'dog': 2, 'was': 1}
```

### Exercise 2: Student Grade Manager
```python
class GradeManager:
    def __init__(self):
        self.students = {}
    
    def add_student(self, student_id, name):
        """Add a new student."""
        self.students[student_id] = {
            "name": name,
            "grades": {},
            "average": 0.0
        }
    
    def add_grade(self, student_id, subject, grade):
        """Add a grade for a student."""
        if student_id in self.students:
            self.students[student_id]["grades"][subject] = grade
            self._update_average(student_id)
    
    def _update_average(self, student_id):
        """Update student's average grade."""
        grades = self.students[student_id]["grades"]
        if grades:
            average = sum(grades.values()) / len(grades)
            self.students[student_id]["average"] = round(average, 2)
    
    def get_student_report(self, student_id):
        """Get comprehensive student report."""
        return self.students.get(student_id, "Student not found")
    
    def get_top_students(self, n=3):
        """Get top N students by average grade."""
        sorted_students = sorted(
            self.students.items(),
            key=lambda x: x[1]["average"],
            reverse=True
        )
        return sorted_students[:n]

# Usage example
gm = GradeManager()
gm.add_student("001", "Alice")
gm.add_student("002", "Bob")
gm.add_grade("001", "Math", 95)
gm.add_grade("001", "Science", 92)
gm.add_grade("002", "Math", 87)
gm.add_grade("002", "Science", 94)

print(gm.get_student_report("001"))
print(gm.get_top_students(2))
```

### Exercise 3: Cache Implementation
```python
class LRUCache:
    """Simple Least Recently Used cache implementation."""
    
    def __init__(self, capacity):
        self.capacity = capacity
        self.cache = {}
        self.access_order = []
    
    def get(self, key):
        """Get value from cache."""
        if key in self.cache:
            # Move to end (most recently used)
            self.access_order.remove(key)
            self.access_order.append(key)
            return self.cache[key]
        return None
    
    def put(self, key, value):
        """Put key-value pair in cache."""
        if key in self.cache:
            # Update existing key
            self.cache[key] = value
            self.access_order.remove(key)
            self.access_order.append(key)
        else:
            # Add new key
            if len(self.cache) >= self.capacity:
                # Remove least recently used
                oldest = self.access_order.pop(0)
                del self.cache[oldest]
            
            self.cache[key] = value
            self.access_order.append(key)
    
    def display(self):
        """Display current cache state."""
        print(f"Cache: {self.cache}")
        print(f"Access order: {self.access_order}")

# Test the cache
cache = LRUCache(3)
cache.put("a", 1)
cache.put("b", 2)
cache.put("c", 3)
cache.display()  # Cache: {'a': 1, 'b': 2, 'c': 3}

cache.get("a")   # Access 'a'
cache.put("d", 4)  # This should remove 'b'
cache.display()  # Cache: {'a': 1, 'c': 3, 'd': 4}
```

### Exercise 4: JSON-like Data Processing
```python
def process_nested_data(data, path=""):
    """Recursively process nested dictionary/list structure."""
    results = {}
    
    if isinstance(data, dict):
        for key, value in data.items():
            current_path = f"{path}.{key}" if path else key
            
            if isinstance(value, (dict, list)):
                # Recursively process nested structures
                nested_results = process_nested_data(value, current_path)
                results.update(nested_results)
            else:
                # Store leaf values
                results[current_path] = value
                
    elif isinstance(data, list):
        for index, item in enumerate(data):
            current_path = f"{path}[{index}]"
            
            if isinstance(item, (dict, list)):
                nested_results = process_nested_data(item, current_path)
                results.update(nested_results)
            else:
                results[current_path] = item
    
    return results

# Test with complex nested structure
nested_data = {
    "user": {
        "id": 123,
        "profile": {
            "name": "Alice",
            "contacts": ["alice@email.com", "555-1234"]
        },
        "preferences": {
            "theme": "dark",
            "notifications": True
        }
    },
    "metadata": {
        "created": "2024-01-01",
        "version": "1.0"
    }
}

flattened = process_nested_data(nested_data)
for key, value in flattened.items():
    print(f"{key}: {value}")

# Output:
# user.id: 123
# user.profile.name: Alice
# user.profile.contacts[0]: alice@email.com
# user.profile.contacts[1]: 555-1234
# user.preferences.theme: dark
# user.preferences.notifications: True
# metadata.created: 2024-01-01
# metadata.version: 1.0
```

---

## Summary

Python dictionaries are powerful, versatile data structures that provide:

- **Fast O(1) average-case access** for key-based operations
- **Flexible data storage** with any immutable type as keys
- **Rich method set** for manipulation and querying
- **Memory-efficient implementation** in modern Python versions
- **Intuitive syntax** for common programming patterns

Master dictionaries to write more efficient, readable Python code for data processing, caching, configuration management, and algorithm implementation.
