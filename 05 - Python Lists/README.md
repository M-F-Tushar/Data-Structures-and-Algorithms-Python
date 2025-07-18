# Complete Python Lists Guide

## Table of Contents
1. [What is a List?](#what-is-a-list)
2. [Creating Lists](#creating-lists)
3. [Accessing and Traversing Lists](#accessing-and-traversing-lists)
4. [Updating and Inserting Elements](#updating-and-inserting-elements)
5. [Slicing Lists](#slicing-lists)
6. [Deleting Elements](#deleting-elements)
7. [Searching in Lists](#searching-in-lists)
8. [List Operations and Functions](#list-operations-and-functions)
9. [Lists and Strings](#lists-and-strings)
10. [Common Pitfalls and How to Avoid Them](#common-pitfalls-and-how-to-avoid-them)
11. [Lists vs Arrays](#lists-vs-arrays)
12. [Time and Space Complexity](#time-and-space-complexity)
13. [Python List Comprehension](#Python-List-Comprehension)
---

## What is a List?

A **list** is a built-in data structure in Python that holds an ordered collection of items. Think of it like a shopping list where you have items separated by commas instead of new lines.

### Key Characteristics:
- **Ordered**: Elements maintain their position as declared
- **Mutable**: You can change, add, or remove elements
- **Flexible**: Can store different data types in the same list
- **Indexed**: Elements can be accessed by their position (starting from 0)

---

## Creating Lists

### Basic List Creation

**Example 1: List of Integers**
```python
integers = [1, 2, 3, 4]
print(integers)  # Output: [1, 2, 3, 4]
```

**Example 2: List of Strings**
```python
stringList = ["milk", "cheese", "butter"]
print(stringList)  # Output: ['milk', 'cheese', 'butter']
```

**Example 3: Mixed Data Types**
```python
mixedList = [1, 2.5, "spam"]
print(mixedList)  # Output: [1, 2.5, 'spam']
```

**Example 4: Nested Lists**
```python
nestedList = [1, 2, 3, [4, 5], "test"]
print(nestedList)  # Output: [1, 2, 3, [4, 5], 'test']
print(len(nestedList))  # Output: 5 (nested list counts as one element)
```

**Example 5: Empty List**
```python
emptyList = []
print(emptyList)  # Output: []
```

### Time and Space Complexity of Creation:
- **Empty list**: O(1) time, O(1) space
- **List with n elements**: O(n) time, O(n) space

---

## Accessing and Traversing Lists

### Accessing Elements by Index

**Example 1: Basic Access**
```python
shopping_list = ["milk", "cheese", "butter"]

# Access first element (index 0)
print(shopping_list[0])  # Output: milk

# Access second element (index 1)
print(shopping_list[1])  # Output: cheese

# Access last element using negative index
print(shopping_list[-1])  # Output: butter
print(shopping_list[-2])  # Output: cheese
```

**Example 2: Index Out of Range**
```python
shopping_list = ["milk", "cheese", "butter"]

# This will cause an error
# print(shopping_list[3])  # IndexError: list index out of range
```

### Checking if Element Exists

**Example 3: Using 'in' Operator**
```python
shopping_list = ["milk", "cheese", "butter"]

print("milk" in shopping_list)    # Output: True
print("bread" in shopping_list)   # Output: False
```

### Traversing Lists

**Example 4: Simple Traversal**
```python
shopping_list = ["milk", "cheese", "butter"]

# Method 1: Direct iteration
for item in shopping_list:
    print(item)
# Output: milk, cheese, butter (each on new line)

# Method 2: Using index
for i in range(len(shopping_list)):
    shopping_list[i] = shopping_list[i] + " ✓"
    
print(shopping_list)  # Output: ['milk ✓', 'cheese ✓', 'butter ✓']
```

---

## Updating and Inserting Elements

### Updating Elements

**Example 1: Update by Index**
```python
myList = [1, 2, 3, 4, 5, 6, 7]
print("Original:", myList)  # Output: [1, 2, 3, 4, 5, 6, 7]

# Update third element (index 2)
myList[2] = 33
print("After update:", myList)  # Output: [1, 2, 33, 4, 5, 6, 7]
```

**Time Complexity**: O(1) - Direct access by index
**Space Complexity**: O(1) - No extra memory needed

### Inserting Elements

**Example 2: Insert at Beginning**
```python
myList = [1, 2, 3, 4, 5]
print("Original:", myList)

# Insert at beginning (index 0)
myList.insert(0, 11)
print("After insert:", myList)  # Output: [11, 1, 2, 3, 4, 5]
```

**Example 3: Insert at Specific Position**
```python
myList = [1, 2, 3, 4, 5]
print("Original:", myList)

# Insert at index 3
myList.insert(3, 15)
print("After insert:", myList)  # Output: [1, 2, 3, 15, 4, 5]
```

**Example 4: Append at End**
```python
myList = [1, 2, 3, 4, 5]
print("Original:", myList)

# Append at end
myList.append(55)
print("After append:", myList)  # Output: [1, 2, 3, 4, 5, 55]
```

**Example 5: Extend with Another List**
```python
myList = [1, 2, 3, 4, 5]
newList = [11, 12, 13, 14]
print("Original:", myList)

# Extend with another list
myList.extend(newList)
print("After extend:", myList)  # Output: [1, 2, 3, 4, 5, 11, 12, 13, 14]
```

### Time Complexity Summary:
- **insert()**: O(n) - Elements need to shift
- **append()**: O(1) - No shifting needed
- **extend()**: O(n) - Depends on size of extending list

---

## Slicing Lists

Slicing allows you to select portions of a list using the syntax `[start:end]` (end is exclusive).

**Example 1: Basic Slicing**
```python
myList = ['A', 'B', 'C', 'D', 'E', 'F']

# Get first two elements
print(myList[0:2])  # Output: ['A', 'B']

# Same result, start can be omitted
print(myList[:2])   # Output: ['A', 'B']

# From index 2 to end
print(myList[2:])   # Output: ['C', 'D', 'E', 'F']

# All elements
print(myList[:])    # Output: ['A', 'B', 'C', 'D', 'E', 'F']
```

**Example 2: Update Multiple Elements**
```python
myList = ['A', 'B', 'C', 'D', 'E', 'F']
print("Original:", myList)

# Update first two elements
myList[0:2] = ['X', 'Y']
print("After update:", myList)  # Output: ['X', 'Y', 'C', 'D', 'E', 'F']
```

---

## Deleting Elements

### Method 1: pop() - Remove by Index

**Example 1: Remove Last Element**
```python
myList = ['A', 'B', 'C', 'D', 'E', 'F']
print("Original:", myList)

# Remove and return last element
removed = myList.pop()
print("Removed:", removed)      # Output: F
print("After pop:", myList)     # Output: ['A', 'B', 'C', 'D', 'E']
```

**Example 2: Remove Specific Index**
```python
myList = ['A', 'B', 'C', 'D', 'E', 'F']
print("Original:", myList)

# Remove element at index 1
removed = myList.pop(1)
print("Removed:", removed)      # Output: B
print("After pop:", myList)     # Output: ['A', 'C', 'D', 'E', 'F']
```

### Method 2: del - Delete by Index

**Example 3: Delete Single Element**
```python
myList = ['A', 'B', 'C', 'D', 'E', 'F']
print("Original:", myList)

# Delete element at index 1
del myList[1]
print("After del:", myList)     # Output: ['A', 'C', 'D', 'E', 'F']
```

**Example 4: Delete Multiple Elements**
```python
myList = ['A', 'B', 'C', 'D', 'E', 'F']
print("Original:", myList)

# Delete elements from index 2 to 4
del myList[2:4]
print("After del:", myList)     # Output: ['A', 'B', 'E', 'F']
```

### Method 3: remove() - Remove by Value

**Example 5: Remove by Value**
```python
myList = ['A', 'B', 'C', 'D', 'E', 'F']
print("Original:", myList)

# Remove first occurrence of 'C'
myList.remove('C')
print("After remove:", myList)  # Output: ['A', 'B', 'D', 'E', 'F']
```

### Time Complexity:
- **pop()** from end: O(1)
- **pop()** from beginning/middle: O(n)
- **del**: O(n) - Elements need to shift
- **remove()**: O(n) - Must search then shift

---

## Searching in Lists

### Method 1: Using 'in' Operator

**Example 1: Check if Element Exists**
```python
myList = [10, 20, 30, 40, 50, 60, 70, 80, 90]
target = 50

if target in myList:
    print(f"{target} is in the list")    # Output: 50 is in the list
else:
    print(f"{target} is not in the list")
```

### Method 2: Linear Search Function

**Example 2: Find Index of Element**
```python
def linear_search(p_list, p_target):
    for i, value in enumerate(p_list):
        if value == p_target:
            return i
    return -1

myList = [10, 20, 30, 40, 50, 60, 70, 80, 90]
target = 50

result = linear_search(myList, target)
print(f"Index of {target}: {result}")  # Output: Index of 50: 4

# Search for non-existent element
result = linear_search(myList, 500)
print(f"Index of 500: {result}")       # Output: Index of 500: -1
```

### Time Complexity:
- **in operator**: O(n) - Linear search
- **linear_search()**: O(n) - Must check each element

---

## List Operations and Functions

### Operations

**Example 1: Concatenation with + Operator**
```python
A = [1, 2, 3]
B = [4, 5, 6]
C = A + B
print(C)  # Output: [1, 2, 3, 4, 5, 6]
```

**Example 2: Repetition with * Operator**
```python
A = [0, 1]
result = A * 4
print(result)  # Output: [0, 1, 0, 1, 0, 1, 0, 1]
```

### Built-in Functions

**Example 3: Common List Functions**
```python
myList = [0, 1, 2, 3, 4, 5, 6]

# Length
print(len(myList))    # Output: 7

# Maximum value
print(max(myList))    # Output: 6

# Minimum value
print(min(myList))    # Output: 0

# Sum of elements
print(sum(myList))    # Output: 21

# Average (using combination of functions)
average = sum(myList) / len(myList)
print(average)        # Output: 3.0
```

### Practical Example: Interactive Number Average

**Example 4: User Input Processing**
```python
def calculate_average():
    numbers = []
    
    while True:
        user_input = input("Enter a number (or 'done' to finish): ")
        if user_input == 'done':
            break
        numbers.append(float(user_input))
    
    if numbers:
        average = sum(numbers) / len(numbers)
        print(f"Average: {average}")
    else:
        print("No numbers entered")

# Example usage:
# calculate_average()
```

---

## Lists and Strings

### Converting String to List

**Example 1: String to Character List**
```python
a = "spam"
b = list(a)
print(b)  # Output: ['s', 'p', 'a', 'm']
```

**Example 2: String to Word List**
```python
sentence = "spam spam spam"
words = sentence.split()
print(words)  # Output: ['spam', 'spam', 'spam']
```

**Example 3: Custom Delimiter**
```python
text = "spam-one-spam-two"
delimiter = "-"
parts = text.split(delimiter)
print(parts)  # Output: ['spam', 'one', 'spam', 'two']
```

### Converting List to String

**Example 4: Join List Elements**
```python
words = ['spam', 'one', 'spam', 'two']
delimiter = "-"
result = delimiter.join(words)
print(result)  # Output: spam-one-spam-two
```

---

## Common Pitfalls and How to Avoid Them

### Pitfall 1: Methods Return None

**❌ Wrong Way:**
```python
myList = [3, 1, 4, 1, 5]
sortedList = myList.sort()  # sort() returns None!
print(sortedList)  # Output: None
```

**✅ Correct Way:**
```python
myList = [3, 1, 4, 1, 5]
myList.sort()  # Modifies original list
print(myList)  # Output: [1, 1, 3, 4, 5]

# Or use sorted() to keep original
original = [3, 1, 4, 1, 5]
sortedList = sorted(original)
print(original)     # Output: [3, 1, 4, 1, 5] (unchanged)
print(sortedList)   # Output: [1, 1, 3, 4, 5]
```

### Pitfall 2: Mixing Append and Concatenation

**❌ Wrong Way:**
```python
myList = [1, 2, 3]
myList.append([4, 5])  # Creates nested list
print(myList)  # Output: [1, 2, 3, [4, 5]]
```

**✅ Correct Way:**
```python
myList = [1, 2, 3]
myList.extend([4, 5])  # Adds elements individually
print(myList)  # Output: [1, 2, 3, 4, 5]
```

### Pitfall 3: Modifying Original List

**❌ Problem:**
```python
original = [3, 1, 4, 1, 5]
original.sort()  # Modifies original
print(original)  # Output: [1, 1, 3, 4, 5] (original is lost)
```

**✅ Solution:**
```python
original = [3, 1, 4, 1, 5]
backup = original.copy()  # Or original[:]
original.sort()
print("Original:", backup)  # Output: [3, 1, 4, 1, 5]
print("Sorted:", original)  # Output: [1, 1, 3, 4, 5]
```

---

## Lists vs Arrays

### Similarities
- Both are mutable
- Both can be indexed and iterated
- Both support slicing

### Key Differences

**Example 1: Arithmetic Operations**
```python
import numpy as np

# Array - supports arithmetic operations
myArray = np.array([1, 2, 3, 4, 5, 6])
print(myArray / 2)  # Output: [0.5 1.  1.5 2.  2.5 3. ]

# List - does not support arithmetic operations
myList = [1, 2, 3, 4, 5, 6]
# print(myList / 2)  # This would cause an error
```

**Example 2: Data Type Flexibility**
```python
import numpy as np

# List - can mix data types
myList = [1, 2, 3, 'a']
print(myList)  # Output: [1, 2, 3, 'a']

# Array - converts all to same type
myArray = np.array([1, 2, 3, 'a'])
print(myArray)  # Output: ['1' '2' '3' 'a'] (all strings)
```

### When to Use Each:
- **Lists**: General purpose, mixed data types, dynamic operations
- **Arrays**: Mathematical computations, same data type, performance-critical

---

## Time and Space Complexity

### Complete Complexity Table

| Operation | Time Complexity | Space Complexity | Notes |
|-----------|----------------|------------------|--------|
| **Create empty list** | O(1) | O(1) | Just allocates list object |
| **Create list with n elements** | O(n) | O(n) | Must initialize each element |
| **Access element by index** | O(1) | O(1) | Direct memory access |
| **Insert at beginning** | O(n) | O(1) | All elements shift right |
| **Insert at end (append)** | O(1) | O(1) | No shifting needed |
| **Insert at middle** | O(n) | O(1) | Elements after index shift |
| **Delete from beginning** | O(n) | O(1) | All elements shift left |
| **Delete from end (pop)** | O(1) | O(1) | No shifting needed |
| **Delete from middle** | O(n) | O(1) | Elements after index shift |
| **Search (linear)** | O(n) | O(1) | Must check each element |
| **Traverse all elements** | O(n) | O(1) | Visit each element once |

# Python List Comprehension 

## What is List Comprehension?

List comprehension is a unique Python feature that allows you to create new lists from existing sequences (lists, strings, tuples, ranges) in a concise, readable way. It transforms multiple lines of loop code into a single line.

## Basic List Comprehension

### Traditional Loop Approach
```python
# Creating a new list by multiplying each element by 2
previous_list = [1, 2, 3]
new_list = []
for i in previous_list:
    multiply_two = i * 2
    new_list.append(multiply_two)
print(new_list)  # Output: [2, 4, 6]
```

### List Comprehension Approach
```python
# Same result in one line
previous_list = [1, 2, 3]
new_list = [i * 2 for i in previous_list]
print(new_list)  # Output: [2, 4, 6]
```

## List Comprehension Syntax

### Basic Template
```python
new_list = [new_item for item in existing_list]
```

### Component Breakdown
- **`new_item`**: Expression for new elements (what to do with each item)
- **`item`**: Variable representing each element from the original sequence
- **`existing_list`**: The sequence you're iterating over

### Step-by-Step Mapping
1. **`existing_list`** → The source data
2. **`for item in existing_list`** → Loop through each element
3. **`new_item`** → Transform each element using this expression

## Working with Different Sequences

### Lists
```python
numbers = [1, 2, 3, 4, 5]
squares = [x**2 for x in numbers]
print(squares)  # Output: [1, 4, 9, 16, 25]
```

### Strings
```python
language = "Python"
letters = [letter for letter in language]
print(letters)  # Output: ['P', 'y', 't', 'h', 'o', 'n']
```

### Ranges
```python
even_numbers = [x for x in range(0, 10, 2)]
print(even_numbers)  # Output: [0, 2, 4, 6, 8]
```

## Conditional List Comprehension

### Basic Conditional (Filter)
```python
# Syntax: [expression for item in sequence if condition]
numbers = [-1, 10, -20, 5, -90]
positive_numbers = [num for num in numbers if num > 0]
print(positive_numbers)  # Output: [10, 5]
```

### Complex Conditional Example
```python
# Get squares of negative numbers only
numbers = [-1, 10, -20, 5, -90]
negative_squares = [num**2 for num in numbers if num < 0]
print(negative_squares)  # Output: [1, 400, 8100]
```

## Conditional Expressions (If-Else)

### Syntax with If-Else
```python
# [expression_if_true if condition else expression_if_false for item in sequence]
numbers = [-1, 10, -20, 5, -90]
result = [num if num > 0 else 0 for num in numbers]
print(result)  # Output: [0, 10, 0, 5, 0]
```

### Practical Example
```python
numbers = [-1, 10, -20, 5, -90]
result = [num if num > 0 else "negative number" for num in numbers]
print(result)  # Output: ['negative number', 10, 'negative number', 5, 'negative number']
```

## Using Functions in List Comprehension

### Creating Helper Functions
```python
def is_consonant(letter):
    vowels = "aeiou"
    return letter.isalpha() and letter.lower() not in vowels

sentence = "My name is Alfred"
consonants = [char for char in sentence if is_consonant(char)]
print(consonants)  # Output: ['M', 'y', 'n', 'm', 's', 'l', 'f', 'r', 'd']
```

### Using Functions in Expressions
```python
def get_number(number):
    if number > 0:
        return number
    else:
        return "negative number"

numbers = [-1, 10, -20, 5, -90]
result = [get_number(num) for num in numbers]
print(result)  # Output: ['negative number', 10, 'negative number', 5, 'negative number']
```

## Advanced Examples

### Multiple Conditions
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
even_squares = [x**2 for x in numbers if x % 2 == 0 if x > 4]
print(even_squares)  # Output: [36, 64, 100]
```

### String Processing
```python
words = ["python", "java", "javascript", "go"]
capitalized = [word.capitalize() for word in words if len(word) > 4]
print(capitalized)  # Output: ['Python', 'Javascript']
```

### Nested Operations
```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flattened = [num for row in matrix for num in row]
print(flattened)  # Output: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## Best Practices

### When to Use List Comprehension
- ✅ Simple transformations and filtering
- ✅ When it improves code readability
- ✅ For creating new lists from existing sequences

### When to Use Traditional Loops
- ❌ Complex logic that makes comprehension hard to read
- ❌ When you need to perform multiple operations per iteration
- ❌ When debugging complex logic

### Readability Tips
1. Keep expressions simple and clear
2. Use meaningful variable names
3. Break complex logic into helper functions
4. If the comprehension is too long, use traditional loops

## Common Patterns

### Pattern 1: Transform All Elements
```python
# Convert temperatures from Celsius to Fahrenheit
celsius = [0, 20, 30, 40]
fahrenheit = [c * 9/5 + 32 for c in celsius]
print(fahrenheit)  # Output: [32.0, 68.0, 86.0, 104.0]
```

### Pattern 2: Filter and Transform
```python
# Get lengths of words longer than 3 characters
words = ["cat", "dog", "elephant", "mouse", "ant"]
long_word_lengths = [len(word) for word in words if len(word) > 3]
print(long_word_lengths)  # Output: [8, 5]
```

### Pattern 3: Conditional Transformation
```python
# Convert negative numbers to positive, keep positive as is
numbers = [-5, 3, -2, 7, -1]
absolute_values = [abs(num) if num < 0 else num for num in numbers]
print(absolute_values)  # Output: [5, 3, 2, 7, 1]
```


### Performance Tips:
1. **Use append()** instead of insert(0) for better performance
2. **Use pop()** without index for O(1) removal
3. **Consider deque** from collections for frequent beginning operations
4. **Use list comprehensions** for efficient list creation

---

## Summary

Python lists are versatile, mutable data structures perfect for storing ordered collections of items. Key takeaways:

- **Flexible**: Can store different data types
- **Ordered**: Elements maintain their position
- **Mutable**: Can be modified after creation
- **Indexed**: Zero-based indexing for direct access
- **Rich functionality**: Many built-in methods and operations
List comprehension is a powerful Python feature that:
- Reduces code length and improves readability
- Works with any sequence (lists, strings, tuples, ranges)
- Supports conditional filtering and expressions
- Can incorporate function calls for complex logic
- Follows the pattern: `[expression for item in sequence if condition]`

Remember: If your list comprehension becomes too complex or hard to read, it's better to use traditional loops for clarity!
Understanding time complexity helps you choose the right operations for your specific use case, making your code more efficient and scalable.
