# Complete Guide to Arrays in Python

## Table of Contents
1. [What is an Array? ](#what-is-an-array)
2. [Arrays vs Lists in Python](#arrays-vs-lists-in-python)
3. [Types of Arrays](#types-of-arrays)
4. [Arrays in Memory](#arrays-in-memory)
5. [Array Operations](#array-operations)
6. [Time and Space Complexity](#time-and-space-complexity)
7. [Practical Examples](#practical-examples)
8. [Creating Arrays in Detail](#creating-arrays-in-detail)
9. [Detailed Array Operations](#detailed-array-operations)
10. [Complete One-Dimensional Array Practice](#complete-one-dimensional-array-practice)
11. [Two-Dimensional Arrays](#two-dimensional-arrays)
12. [Complete Time and Space Complexity Tables](#complete-time-and-space-complexity-tables)
13. [When to Use/Avoid Arrays](#when-to-useavoid-arrays)
14. [Advanced Examples and Use Cases](#advanced-examples-and-use-cases)

---

## 1. What is an Array?

### Definition
An array is a data structure that stores a collection of elements of the same data type in contiguous memory locations. Each element can be accessed using a unique index.

### Key Properties of Arrays
1. **Homogeneous Data**: All elements must be of the same data type
2. **Contiguous Memory**: Elements are stored next to each other in memory
3. **Indexed Access**: Each element has a unique index starting from 0
4. **Fixed Size**: Once created, the size typically cannot be changed

### Real-World Analogy:  Box of Macarons
Think of an array like a box of macarons: 
- The box is designed specifically for macarons (specific data type)
- All macarons are placed next to each other with no gaps (contiguous)
- Each macaron has a specific position that can be identified (indexed)
- You can't fit a cream puff in a macaron box (type restriction)

### Why Do We Need Arrays?
Instead of creating individual variables like: 
```python
number1 = 10
number2 = 20
number3 = 30
# ...  imagine doing this for 500 numbers! 
```

We can use an array to store all values in one structure:
```python
numbers = [10, 20, 30, 40, 50]  # Much more efficient! 
```

---

## 2. Arrays vs Lists in Python

### Important Note
**Arrays are not native data structures in Python. ** Instead, Python uses **lists**, which are more flexible but similar in concept.

### Creating Arrays in Python

#### Method 1: Using Python's `array` Module
```python
import array

# Create an array of integers
my_array = array.array('i', [1, 2, 3, 4, 5])
print(my_array)  # array('i', [1, 2, 3, 4, 5])

# Create an empty array
empty_array = array. array('i')
print(empty_array)  # array('i')
```

#### Method 2: Using NumPy (More Efficient)
```python
import numpy as np

# Create a NumPy array
np_array = np.array([1, 2, 3, 4], dtype=int)
print(np_array)  # [1 2 3 4]

# Create an array with specific data type
np_array1 = np.array([1, 2, 3, 4])
print(np_array1)  # [1 2 3 4]
```

### Array Type Codes (Python array module)

| Type Code | C Type | Python Type | Size (bytes) |
|-----------|---------|-------------|--------------|
| 'b' | signed char | int | 1 |
| 'B' | unsigned char | int | 1 |
| 'h' | signed short | int | 2 |
| 'H' | unsigned short | int | 2 |
| 'i' | signed int | int | 2 |
| 'I' | unsigned int | int | 2 |
| 'l' | signed long | int | 4 |
| 'L' | unsigned long | int | 4 |
| 'f' | float | float | 4 |
| 'd' | double | float | 8 |

---

## 3. Types of Arrays

### 3.1 One-Dimensional Array

#### Definition
A one-dimensional array is a linear collection of elements arranged in a single row. 

#### Structure
```
Index:   [0] [1] [2] [3] [4] [5] [6] [7] [8]
Values: [5] [4] [10][11][8] [11][68][87][12]
```

#### Accessing Elements
```python
import array

# Create a 1D array
arr = array.array('i', [5, 4, 10, 11, 8, 11, 68, 87, 12])

# Access elements using index
print(arr[0])  # Output: 5 (first element)
print(arr[2])  # Output: 10 (third element)
print(arr[5])  # Output: 11 (sixth element)

# Access using variable
index = 3
print(arr[index])  # Output: 11
```

### 3.2 Two-Dimensional Array

#### Definition
A two-dimensional array is an array of arrays, representing data in rows and columns (like a matrix).

#### Structure
```
        Column Index
        [0] [1] [2] [3] [4] [5] [6] [7] [8]
Row [0]  1  33  55  91  20  51  62  74  13
Row [1]  5   4  10  11   8  11  68  87  12
Row [2] 24  50  37  40  48  30  59  81  93
```

#### Accessing Elements
```python
import numpy as np

# Create a 2D array
arr_2d = np.array([
    [1, 33, 55, 91, 20],
    [5, 4, 10, 11, 8],
    [24, 50, 37, 40, 48]
])

# Access elements using [row][column] format
print(arr_2d[0][4])  # Output: 20 (row 0, column 4)
print(arr_2d[2][5])  # Output: 30 (row 2, column 5)

# Alternative access method
print(arr_2d[1, 2])  # Output: 10 (row 1, column 2)
```

#### Key Point
**Always specify row index first, then column index! **

### 3.3 Three-Dimensional Array

#### Definition
A three-dimensional array can be visualized as a cube or multiple 2D arrays stacked together.

#### Structure
Think of it as having depth, rows, and columns:
- **Depth**: Which "layer" of the cube
- **Row**:  Which row in that layer
- **Column**: Which column in that row

#### Accessing Elements
```python
import numpy as np

# Create a 3D array
arr_3d = np.array([
    [[0, 1, 2], [3, 4, 5]],      # Depth 0
    [[6, 7, 8], [9, 10, 11]],    # Depth 1
    [[12, 13, 14], [15, 16, 17]] # Depth 2
])

# Access elements using [depth][row][column] format
print(arr_3d[0][0][1])  # Output: 1 (depth 0, row 0, column 1)
print(arr_3d[2][0][2])  # Output: 14 (depth 2, row 0, column 2)
```

#### Usage Note
One-dimensional and two-dimensional arrays are widely used in programming, while three-dimensional arrays are used less frequently. 

---

## 4. Arrays in Memory

### 4.1 One-Dimensional Array Memory Layout

#### How it works: 
- When you create an array of 9 elements, the system allocates 9 contiguous memory cells
- The starting location depends on system availability
- All elements are guaranteed to be next to each other

#### Memory Representation: 
```
Array:  [5, 4, 10, 11, 8, 11, 68, 87, 12]

Memory Layout: 
┌────┬────┬────┬────┬────┬────┬────┬────┬────┐
│ 5  │ 4  │ 10 │ 11 │ 8  │ 11 │ 68 │ 87 │ 12 │
└────┴────┴────┴────┴────┴────┴────┴────┴────┘
```

### 4.2 Two-Dimensional Array Memory Layout

#### Visual vs Reality:
While we visualize 2D arrays as: 
```
┌─────┬─────┬─────┐
│  1  │  2  │  3  │
├─────┼─────┼─────┤
│  4  │  5  │  6  │
├─────┼─────┼─────┤
│  7  │  8  │  9  │
└─────┴─────┴─────┘
```

#### Actual Memory Layout:
```
Row 1    Row 2    Row 3
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│  1  │  2  │  3  │  4  │  5  │  6  │  7  │  8  │  9  │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘
```

The system combines all rows into a single linear sequence in memory.

### 4.3 Three-Dimensional Array Memory Layout

#### Conceptual Structure:
```
Depth 0: [[0, 1, 2], [3, 4, 5]]
Depth 1: [[6, 7, 8], [9, 10, 11]]
Depth 2: [[12, 13, 14], [15, 16, 17]]
```

#### Memory Layout:
```
┌────┬────┬────┬────┬────┬────┬────┬────┬────┬────┬────┬────┬────┬────┬────┬────┬────┬────┐
│ 0  │ 1  │ 2  │ 3  │ 4  │ 5  │ 6  │ 7  │ 8  │ 9  │ 10 │ 11 │ 12 │ 13 │ 14 │ 15 │ 16 │ 17 │
└────┴────┴────┴────┴────┴────┴────┴────┴────┴────┴────┴────┴────┴────┴────┴────┴────┴────┘
```

#### Key Insight
**All arrays, regardless of dimensions, are stored as one-dimensional sequences in physical memory! **

---

## 5. Array Operations

### 5.1 Creating Arrays

#### Example 1: Basic Array Creation
```python
import array

# Create an array with initial values
my_array = array.array('i', [1, 2, 3, 4])
print(my_array)  # array('i', [1, 2, 3, 4])

# Create using NumPy
import numpy as np
np_array = np.array([1, 2, 3, 4])
print(np_array)  # [1 2 3 4]
```

### 5.2 Accessing Elements

#### Example 2: Element Access with Error Handling
```python
import array

arr1 = array.array('i', [1, 2, 3, 4, 5, 6])

def accessElement(array, index):
    if index >= len(array):
        print('There is not any element in this index')
    else:
        print(array[index])

# Test the function
accessElement(arr1, 6)  # Error: index out of range
accessElement(arr1, 3)  # Output: 4
```

### 5.3 Searching Elements

#### Example 3: Linear Search Implementation
```python
import array

my_array1 = array.array('i', [1, 2, 3, 4, 5])

def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target: 
            return i
    return -1

# Test the search function
result = linear_search(my_array1, 3)
print(result)  # Output: 2 (index of element 3)

result = linear_search(my_array1, 8)
print(result)  # Output: -1 (element not found)
```

### 5.4 Inserting Elements

#### Example 4: Insert Operation
```python
import array

my_array1 = array.array('i', [1, 2, 3, 4])
print(my_array1)  # array('i', [1, 2, 3, 4])

# Insert element 6 at index 0
my_array1.insert(0, 6)
print(my_array1)  # array('i', [6, 1, 2, 3, 4])
```

### 5.5 Traversing Arrays

#### Example 5: Array Traversal
```python
import array

arr1 = array.array('i', [1, 2, 3, 4, 5, 6])
arr2 = array.array('d', [1.3, 1.5, 1.6])

def traverseArray(array):
    for i in array:
        print(i)

# Traverse both arrays
traverseArray(arr1)
# Output:  1, 2, 3, 4, 5, 6 (each on new line)

traverseArray(arr2)
# Output: 1.3, 1.5, 1.6 (each on new line)
```

### 5.6 Deleting Elements

#### Example 6: Remove Operation
```python
import array

arr1 = array.array('i', [1, 2, 3, 4, 5])
print(arr1)  # array('i', [1, 2, 3, 4, 5])

# Remove element at index 4
arr1.remove(4)  # Removes the value 4, not index 4
print(arr1)  # array('i', [1, 2, 3, 5])
```

---

## 6. Time and Space Complexity

### Complexity Analysis Table

| Operation | Time Complexity | Space Complexity | Explanation |
|-----------|----------------|------------------|-------------|
| Creating an empty array | O(1) | O(1) | Constant time and space |
| Creating array with elements | O(N) | O(N) | Need to process N elements |
| Inserting a value | O(N) | O(1) | May need to shift elements |
| Traversing array | O(N) | O(1) | Visit each element once |
| Accessing element | O(1) | O(1) | Direct index access |
| Searching value | O(N) | O(1) | May need to check all elements |
| Deleting value | O(N) | O(1) | May need to shift elements |

### Detailed Analysis

#### 1. Access Operation:  O(1)
```python
arr = [1, 2, 3, 4, 5]
element = arr[2]  # Always takes same time regardless of array size
```

#### 2. Search Operation: O(N)
```python
def linear_search(arr, target):
    for i in range(len(arr)):  # Worst case: check all N elements
        if arr[i] == target:
            return i
    return -1
```

#### 3. Insert Operation: O(N)
```python
# Inserting at beginning requires shifting all elements
arr. insert(0, new_value)  # O(N) - need to shift N elements
```

---

## 7. Practical Examples

### Example 1: Student Grades Management
```python
import array

# Store student grades
grades = array.array('i', [85, 92, 78, 96, 88])

def calculate_average(grades_array):
    total = sum(grades_array)
    return total / len(grades_array)

def find_highest_grade(grades_array):
    highest = grades_array[0]
    for grade in grades_array:
        if grade > highest:
            highest = grade
    return highest

# Usage
avg = calculate_average(grades)
highest = find_highest_grade(grades)
print(f"Average grade: {avg}")
print(f"Highest grade:  {highest}")
```

### Example 2: Temperature Readings
```python
import array

# Daily temperature readings for a week
temperatures = array.array('f', [23.5, 25.0, 22.8, 26.2, 24.1, 23.9, 25.5])

def find_temperature_range(temp_array):
    min_temp = min(temp_array)
    max_temp = max(temp_array)
    return min_temp, max_temp

def count_above_threshold(temp_array, threshold):
    count = 0
    for temp in temp_array:
        if temp > threshold:
            count += 1
    return count

# Usage
min_temp, max_temp = find_temperature_range(temperatures)
hot_days = count_above_threshold(temperatures, 25.0)

print(f"Temperature range: {min_temp}°C to {max_temp}°C")
print(f"Days above 25°C: {hot_days}")
```

### Example 3: Inventory Management
```python
import array

# Product quantities in inventory
inventory = array.array('i', [50, 30, 75, 20, 45])
product_names = ['Apples', 'Oranges', 'Bananas', 'Grapes', 'Pears']

def update_inventory(inventory_array, product_index, quantity_change):
    if 0 <= product_index < len(inventory_array):
        inventory_array[product_index] += quantity_change
        return True
    return False

def low_stock_alert(inventory_array, threshold=25):
    low_stock_items = []
    for i, quantity in enumerate(inventory_array):
        if quantity < threshold:
            low_stock_items.append(i)
    return low_stock_items

# Usage
update_inventory(inventory, 3, -15)  # Sold 15 grapes
low_stock = low_stock_alert(inventory)

print("Updated inventory:", inventory)
print("Low stock items:", [product_names[i] for i in low_stock])
```

---

## 8. Creating Arrays in Detail

### 8.1 Using the Array Module

#### Creating Empty Arrays
```python
import array

# Create an empty integer array
my_array = array.array('i')
print(my_array)  # array('i')

# Time Complexity: O(1)
# Space Complexity: O(1)
```

#### Creating Arrays with Elements
```python
import array

# Create array with initial values
my_array1 = array.array('i', [1, 2, 3, 4])
print(my_array1)  # array('i', [1, 2, 3, 4])

# Time Complexity: O(N) - must copy N elements
# Space Complexity: O(N) - must allocate space for N elements
```

### 8.2 Using NumPy Module

#### Creating Empty Arrays
```python
import numpy as np

# Create an empty NumPy array
np_array = np.array([], dtype=int)
print(np_array)  # []

# Time Complexity: O(1)
# Space Complexity:  O(1)
```

#### Creating Arrays with Elements
```python
import numpy as np

# Create NumPy array with values
np_array1 = np.array([1, 2, 3, 4])
print(np_array1)  # [1 2 3 4]

# Time Complexity: O(N)
# Space Complexity: O(N)
```

### 8.3 Comparison: Array vs NumPy

| Feature | Array Module | NumPy Module |
|---------|-------------|--------------|
| Installation | Built-in Python | Requires pip install |
| Performance | Good for basic types | Optimized for numerical operations |
| Features | Basic operations | Rich mathematical functions |
| Memory | More efficient than lists | Highly optimized |
| Data Types | Basic types only | Wide range of types |

---

## 9. Detailed Array Operations

### 9.1 Insertion Operations

#### Case 1: Insert at Beginning
```python
import array

arr = array.array('i', [1, 2, 3, 4, 5])
print("Before:", arr)

# Insert 6 at index 0
arr.insert(0, 6)
print("After:", arr)
# Output: array('i', [6, 1, 2, 3, 4, 5])

# Time Complexity: O(N) - all elements shift right
# Space Complexity: O(1) - only one new cell
```

**What happens in memory:**
- Element at index 0 moves to index 1
- Element at index 1 moves to index 2
- All elements shift one position right
- New element takes index 0

#### Case 2: Insert in Middle
```python
import array

arr = array.array('i', [1, 2, 3, 4, 5])

# Insert 6 at index 2
arr.insert(2, 6)
print(arr)
# Output: array('i', [1, 2, 6, 3, 4, 5])

# Time Complexity: O(N) - elements from index 2 onwards shift
# Space Complexity: O(1)
```

#### Case 3: Insert at End
```python
import array

arr = array.array('i', [1, 2, 3, 4, 5])

# Insert 6 at end
arr.insert(5, 6)  # or any index >= length
print(arr)
# Output: array('i', [1, 2, 3, 4, 5, 6])

# Time Complexity: O(1) - no shifting needed
# Space Complexity:  O(1)
```

### 9.2 Traversal Operation

#### Basic Traversal
```python
import array

arr1 = array.array('i', [1, 2, 3, 4, 5, 6])

def traverseArray(array):
    for i in array: 
        print(i)

traverseArray(arr1)
# Output: 
# 1
# 2
# 3
# 4
# 5
# 6

# Time Complexity: O(N) - visit each element
# Space Complexity: O(1) - no extra space needed
```

### 9.3 Accessing Elements

#### Safe Element Access
```python
import array

arr1 = array.array('i', [1, 2, 3, 4, 5, 6])

def accessElement(array, index):
    if index >= len(array):
        print('There is not any element in this index')
    else:
        print(array[index])

# Test cases
accessElement(arr1, 3)  # Output: 4
accessElement(arr1, 6)  # Output: There is not any element in this index

# Time Complexity: O(1) - direct index access
# Space Complexity: O(1)
```

**Key Points:**
- Arrays provide O(1) access time through indexing
- Index starts from 0
- Always validate index before accessing
- This is the main advantage of arrays over other data structures

### 9.4 Searching Elements

#### Linear Search Implementation
```python
import array

my_array1 = array.array('i', [1, 2, 3, 4, 5])

def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target: 
            return i
    return -1

# Test cases
result1 = linear_search(my_array1, 3)
print(result1)  # Output: 2

result2 = linear_search(my_array1, 8)
print(result2)  # Output: -1

# Time Complexity: O(N) - may check all elements
# Space Complexity:  O(1) - no extra space
```

**How Linear Search Works:**
1. Start from first element (index 0)
2. Compare current element with target
3. If match found, return index
4. If not found, move to next element
5. If end reached without finding, return -1

### 9.5 Deleting Elements

#### Understanding Deletion
```python
import array

arr1 = array.array('i', [1, 2, 3, 4, 5, 6])
print("Before:", arr1)

# Remove element with value 4
arr1.remove(4)
print("After:", arr1)
# Output: array('i', [1, 2, 3, 5, 6])

# Time Complexity: O(N) - elements shift left
# Space Complexity: O(1) - no extra space
```

**What happens during deletion:**
```
Initial:  [A, B, C, D, E]
Delete B
Step 1: [A, _, C, D, E]  (B is removed)
Step 2: [A, C, D, E, _]  (All elements after B shift left)
```

#### Important Notes: 
- Cannot leave empty cells in array (violates contiguous property)
- All elements after deleted element shift left
- Deleting last element is most efficient:  O(1)
- `remove()` deletes first occurrence only

```python
import array

# Remove with duplicate values
arr = array.array('i', [11, 2, 3, 11, 4, 5])
arr.remove(11)  # Removes first 11 only
print(arr)  # array('i', [2, 3, 11, 4, 5])
```

---

## 10. Complete One-Dimensional Array Practice

### 10.1 Comprehensive Example with All Operations

```python
from array import *

# Step 1: Create and traverse array
my_array = array('i', [1, 2, 3, 4, 5])
print("Initial array:")
for element in my_array:
    print(element)

# Step 2: Access individual elements
print("\nStep 2 - Access element at index 3:")
print(my_array[3])  # Output: 4

# Step 3: Append element at end
my_array.append(6)
print("\nStep 3 - After append(6):")
print(my_array)  # array('i', [1, 2, 3, 4, 5, 6])

# Step 4: Insert element at specific position
my_array.insert(0, 11)
print("\nStep 4 - After insert(0, 11):")
print(my_array)  # array('i', [11, 1, 2, 3, 4, 5, 6])

# Step 5: Extend array with another array
my_array1 = array('i', [10, 11, 12])
my_array. extend(my_array1)
print("\nStep 5 - After extend:")
print(my_array)

# Step 6: Add elements from list
tempList = [20, 21, 22]
my_array.fromlist(tempList)
print("\nStep 6 - After fromlist:")
print(my_array)

# Step 7: Remove element
my_array.remove(11)  # Removes first occurrence
print("\nStep 7 - After remove(11):")
print(my_array)

# Step 8: Pop last element
my_array.pop()
print("\nStep 8 - After pop():")
print(my_array)

# Step 9: Find index of element
index = my_array.index(21)
print(f"\nStep 9 - Index of 21: {index}")

# Step 10: Reverse array
my_array.reverse()
print("\nStep 10 - After reverse():")
print(my_array)

# Step 11: Buffer info
print("\nStep 11 - Buffer info:")
print(my_array.buffer_info())
# Output:  (memory_address, number_of_elements)

# Step 12: Count occurrences
my_array.append(11)
count = my_array.count(11)
print(f"\nStep 12 - Count of 11: {count}")

# Step 13: Convert to string and back
strTemp = my_array.tobytes()  # Updated method name
print("\nStep 13 - Converted to bytes (shows as bytes)")

ints = array('i')
ints.frombytes(strTemp)  # Updated method name
print("Converted back to array:")
print(ints)

# Step 14: Convert to list
list_version = my_array.tolist()
print("\nStep 14 - As list:")
print(list_version)

# Step 15: Array slicing
print("\nStep 15 - Slicing examples:")
print("First 3 elements:", my_array[:3])
print("Elements from index 2:", my_array[2:])
print("Elements 1 to 4:", my_array[1:5])
```

### 10.2 Built-in Array Methods Summary

| Method | Description | Time Complexity |
|--------|-------------|-----------------|
| `append(x)` | Add x to end | O(1) |
| `insert(i, x)` | Insert x at index i | O(N) |
| `extend(arr)` | Add all elements from arr | O(K) where K is length of arr |
| `fromlist(list)` | Append items from list | O(K) |
| `remove(x)` | Remove first occurrence of x | O(N) |
| `pop()` | Remove and return last item | O(1) |
| `index(x)` | Return index of first occurrence | O(N) |
| `reverse()` | Reverse array in place | O(N) |
| `count(x)` | Count occurrences of x | O(N) |
| `tolist()` | Convert to list | O(N) |
| `buffer_info()` | Get memory info | O(1) |
| `tobytes()` | Convert to bytes | O(N) |
| `frombytes()` | Append from bytes | O(N) |

---

## 11. Two-Dimensional Arrays

### 11.1 Understanding 2D Arrays

A two-dimensional array is essentially an array of arrays, representing data in rows and columns like a matrix.

**Visual Representation:**
```
        Column 0  Column 1  Column 2  Column 3
Row 0     11        15        10         6
Row 1     10        14        11         5
Row 2     12        17        12         8
Row 3     15        16        14         9
```

**Real-World Use Cases:**
- Recording daily temperatures
- Game boards (chess, tic-tac-toe)
- Image processing (pixels)
- Spreadsheet data
- Seating arrangements

### 11.2 Creating Two-Dimensional Arrays

```python
import numpy as np

# Example:  Daily temperature readings (4 days, 4 times per day)
# Day 1: 11°C, 15°C, 10°C, 6°C
# Day 2: 10°C, 14°C, 11°C, 5°C
# Day 3: 12°C, 17°C, 12°C, 8°C
# Day 4: 15°C, 16°C, 14°C, 9°C

two_dimensional_array = np.array([
    [11, 15, 10, 6],
    [10, 14, 11, 5],
    [12, 17, 12, 8],
    [15, 16, 14, 9]
])

print(two_dimensional_array)
# Output:
# [[11 15 10  6]
#  [10 14 11  5]
#  [12 17 12  8]
#  [15 16 14  9]]

# Time Complexity: O(M*N) where M=rows, N=columns
# Space Complexity: O(M*N)
```

### 11.3 Inserting Rows and Columns

#### Insert Column
```python
import numpy as np

two_dimensional_array = np. array([
    [11, 15, 10, 6],
    [10, 14, 11, 5],
    [12, 17, 12, 8],
    [15, 16, 14, 9]
])

# Insert column at beginning (index 0)
new_array = np.insert(two_dimensional_array, 0, [1, 2, 3, 4], axis=1)
print("After inserting column:")
print(new_array)
# Output:
# [[ 1 11 15 10  6]
#  [ 2 10 14 11  5]
#  [ 3 12 17 12  8]
#  [ 4 15 16 14  9]]

# Time Complexity: O(M*N) - all elements shift
# Space Complexity: O(M*N) - new array created
```

**What Happens:**
- Original first column shifts to second position
- All other columns shift one position right
- New column takes first position

#### Insert Row
```python
import numpy as np

two_dimensional_array = np.array([
    [11, 15, 10, 6],
    [10, 14, 11, 5],
    [12, 17, 12, 8],
    [15, 16, 14, 9]
])

# Insert row at beginning (index 0)
new_array = np.insert(two_dimensional_array, 0, [1, 2, 3, 4], axis=0)
print("After inserting row:")
print(new_array)
# Output:
# [[ 1  2  3  4]
#  [11 15 10  6]
#  [10 14 11  5]
#  [12 17 12  8]
#  [15 16 14  9]]

# Time Complexity: O(M*N)
# Space Complexity: O(M*N)
```

#### Append Row or Column at End
```python
import numpy as np

two_dimensional_array = np.array([
    [11, 15, 10, 6],
    [10, 14, 11, 5],
    [12, 17, 12, 8]
])

# Append row at end
new_array = np. append(two_dimensional_array, [[1, 2, 3, 4]], axis=0)
print("After appending row:")
print(new_array)

# Append column at end
new_array2 = np.append(two_dimensional_array, [[1], [2], [3]], axis=1)
print("\nAfter appending column:")
print(new_array2)

# Time Complexity: O(M*N)
# Space Complexity: O(M*N)
```

### 11.4 Accessing Elements in 2D Arrays

```python
import numpy as np

arr_2d = np.array([
    [11, 15, 10, 6],
    [10, 14, 11, 5],
    [12, 17, 12, 8]
])

def accessElement(array, row_index, col_index):
    # Validate indices
    if row_index >= len(array) or col_index >= len(array[0]):
        print('Incorrect index')
    else:
        print(array[row_index][col_index])

# Test cases
accessElement(arr_2d, 1, 2)  # Output: 11
accessElement(arr_2d, 0, 3)  # Output: 6
accessElement(arr_2d, 5, 2)  # Output: Incorrect index

# Time Complexity:  O(1) - direct access
# Space Complexity: O(1)
```

**Key Points:**
- First index = row (vertical position)
- Second index = column (horizontal position)
- Index validation is essential
- Access is O(1) regardless of array size

### 11.5 Traversing 2D Arrays

```python
import numpy as np

arr_2d = np.array([
    [11, 15, 10, 6],
    [10, 14, 11, 5],
    [12, 17, 12, 8]
])

def traverseTDArray(array):
    # Outer loop:  iterate through rows
    for i in range(len(array)):
        # Inner loop: iterate through columns
        for j in range(len(array[0])):
            print(array[i][j])

traverseTDArray(arr_2d)
# Output:
# 11
# 15
# 10
# 6
# 10
# 14
# 11
# 5
# 12
# 17
# 12
# 8

# Time Complexity: O(M*N) - visit each element
# Space Complexity: O(1) - no extra space
```

**Traversal Pattern:**
1. Start at [0][0] (first row, first column)
2. Move through all columns in first row
3. Move to next row, repeat
4. Continue until all elements visited

### 11.6 Searching in 2D Arrays

```python
import numpy as np

arr_2d = np.array([
    [11, 15, 10, 6],
    [10, 14, 44, 5],
    [12, 17, 12, 8]
])

def search2DArray(array, value):
    # Search through rows
    for i in range(len(array)):
        # Search through columns
        for j in range(len(array[0])):
            if array[i][j] == value:
                return f'The value is located at index {i},{j}'
    return 'The element is not found'

# Test cases
print(search2DArray(arr_2d, 44))  # Output: The value is located at index 1,2
print(search2DArray(arr_2d, 14))  # Output: The value is located at index 1,1
print(search2DArray(arr_2d, 55))  # Output: The element is not found

# Time Complexity: O(M*N) - worst case check all elements
# Space Complexity:  O(1)
```

### 11.7 Deleting Rows and Columns

```python
import numpy as np

two_dimensional_array = np.array([
    [11, 15, 10, 6],
    [10, 14, 11, 5],
    [12, 17, 12, 8],
    [15, 16, 14, 9]
])

# Delete first row (index 0)
new_array = np.delete(two_dimensional_array, 0, axis=0)
print("After deleting first row:")
print(new_array)
# Output:
# [[10 14 11  5]
#  [12 17 12  8]
#  [15 16 14  9]]

# Delete first column (index 0)
new_array2 = np. delete(two_dimensional_array, 0, axis=1)
print("\nAfter deleting first column:")
print(new_array2)
# Output:
# [[15 10  6]
#  [14 11  5]
#  [17 12  8]
#  [16 14  9]]

# Delete second column (index 1)
new_array3 = np.delete(two_dimensional_array, 1, axis=1)
print("\nAfter deleting second column:")
print(new_array3)

# Time Complexity: O(M*N)
# Space Complexity: O(M*N)
```

**Important Notes:**
- NumPy creates a new array (doesn't delete in place)
- Original data (minus deleted row/column) is copied to new array
- `axis=0`: delete row
- `axis=1`: delete column

---

## 12. Complete Time and Space Complexity Tables

### 12.1 One-Dimensional Array Operations

| Operation | Time Complexity | Space Complexity | Notes |
|-----------|----------------|------------------|-------|
| Create empty array | O(1) | O(1) | No elements allocated |
| Create with N elements | O(N) | O(N) | Must copy/allocate N elements |
| Insert at beginning | O(N) | O(1) | All elements shift right |
| Insert in middle | O(N) | O(1) | Elements after index shift |
| Insert at end | O(1) | O(1) | No shifting needed |
| Traverse array | O(N) | O(1) | Visit each element once |
| Access element | O(1) | O(1) | Direct index access |
| Search for value | O(N) | O(1) | Linear search |
| Delete element | O(N) | O(1) | Elements shift left |
| Delete last element | O(1) | O(1) | No shifting needed |

### 12.2 Two-Dimensional Array Operations

| Operation | Time Complexity | Space Complexity | Notes |
|-----------|----------------|------------------|-------|
| Create empty 2D array | O(1) | O(1) | No elements allocated |
| Create with elements | O(M*N) | O(M*N) | M rows, N columns |
| Insert row | O(M*N) | O(M*N) | Create new array, copy all |
| Insert column | O(M*N) | O(M*N) | Create new array, copy all |
| Append row at end | O(M*N) | O(M*N) | Create new array |
| Append column at end | O(M*N) | O(M*N) | Create new array |
| Access element | O(1) | O(1) | Direct index access |
| Traverse array | O(M*N) | O(1) | Visit each element |
| Search for value | O(M*N) | O(1) | Check each element |
| Delete row | O(M*N) | O(M*N) | Create new array, copy |
| Delete column | O(M*N) | O(M*N) | Create new array, copy |

---

## 13. When to Use/Avoid Arrays

### 13.1 When to Use Arrays ✅

#### 1. Storing Multiple Variables of Same Type
```python
# Instead of:
temp1 = 20
temp2 = 22
temp3 = 21
# ...  (imagine 1000 variables!)

# Use array:
temperatures = array. array('i', [20, 22, 21, ... ])  # Much better!
```

**Benefits:**
- Cleaner code
- Easier to manage
- Can use loops to process data
- More maintainable

#### 2. Random Access Requirements
```python
import array

# Large dataset with 10,000 elements
data = array.array('i', range(10000))

# Access any element in O(1) time
element = data[5000]  # Instant access, regardless of position
```

**Benefits:**
- O(1) access time for any element
- Perfect for applications needing quick lookups
- Efficient for algorithms requiring random access

#### 3. Memory-Efficient Storage
```python
import array

# Arrays are more memory efficient than lists for numeric data
int_array = array.array('i', [1, 2, 3, 4, 5])  # More efficient
int_list = [1, 2, 3, 4, 5]  # Less efficient (more overhead)
```

### 13.2 When to Avoid Arrays ❌

#### 1. Mixed Data Types Needed
```python
# Arrays don't work well with mixed types
# Use lists instead:
mixed_data = [1, "hello", 3.14, True]  # List allows this
# array.array cannot do this efficiently
```

#### 2. Frequent Insertions/Deletions
```python
# Avoid arrays if you need frequent insertions/deletions
# Each insertion/deletion at beginning/middle is O(N)

# Bad use case:
data = array.array('i', [1, 2, 3, 4, 5])
# Frequent operations like: 
data. insert(0, 10)  # O(N) - very slow
data.remove(3)      # O(N) - very slow

# Consider using other data structures like:
# - Linked lists for frequent insertions/deletions
# - Deques for operations at both ends
```

#### 3. Unknown or Dynamic Size
```python
# Arrays reserve fixed memory
# If size varies greatly, may waste space or require frequent resizing

# Problem scenario:
large_array = array.array('i', [0] * 10000)  # Reserved for 10,000
# But only use 100 elements → waste of 9,900 spaces

# Better:  Use dynamic data structures when size is unpredictable
```

### 13.3 Decision Guide

**Use Arrays When:**
- ✅ All elements are same data type
- ✅ Size is known or relatively stable
- ✅ Need fast random access (O(1))
- ✅ Minimal insertions/deletions
- ✅ Memory efficiency is important

**Avoid Arrays When:**
- ❌ Need mixed data types
- ❌ Frequent insertions/deletions
- ❌ Size varies dramatically
- ❌ Primarily adding/removing at beginning
- ❌ Need to frequently grow/shrink structure

---

## 14. Advanced Examples and Use Cases

### 14.1 Temperature Analysis System
```python
import numpy as np

# Weekly temperature data (7 days, 4 readings per day)
weekly_temps = np.array([
    [22, 25, 28, 24],  # Monday
    [21, 24, 27, 23],  # Tuesday
    [23, 26, 29, 25],  # Wednesday
    [20, 23, 26, 22],  # Thursday
    [22, 25, 28, 24],  # Friday
    [24, 27, 30, 26],  # Saturday
    [23, 26, 29, 25]   # Sunday
])

def analyze_temperatures(temps):
    # Average daily temperature
    daily_averages = np.mean(temps, axis=1)
    print("Daily Averages:", daily_averages)
    
    # Maximum temperature each day
    daily_max = np.max(temps, axis=1)
    print("Daily Maximums:", daily_max)
    
    # Minimum temperature each day
    daily_min = np. min(temps, axis=1)
    print("Daily Minimums:", daily_min)
    
    # Overall weekly average
    weekly_avg = np. mean(temps)
    print(f"Weekly Average: {weekly_avg:. 2f}°C")
    
    # Hottest reading
    hottest = np.max(temps)
    print(f"Hottest Reading: {hottest}°C")

analyze_temperatures(weekly_temps)
```

### 14.2 Simple Game Board
```python
import numpy as np

# 3x3 Tic-Tac-Toe board
def create_game_board():
    return np.array([
        ['-', '-', '-'],
        ['-', '-', '-'],
        ['-', '-', '-']
    ])

def display_board(board):
    for row in board:
        print(' '.join(row))
    print()

def make_move(board, row, col, player):
    if board[row][col] == '-':
        board[row][col] = player
        return True
    return False

def check_winner(board):
    # Check rows
    for row in board: 
        if row[0] == row[1] == row[2] != '-':
            return row[0]
    
    # Check columns
    for col in range(3):
        if board[0][col] == board[1][col] == board[2][col] != '-':
            return board[0][col]
    
    # Check diagonals
    if board[0][0] == board[1][1] == board[2][2] != '-': 
        return board[0][0]
    if board[0][2] == board[1][1] == board[2][0] != '-':
        return board[0][2]
    
    return None

# Example game
board = create_game_board()
display_board(board)

make_move(board, 0, 0, 'X')
make_move(board, 1, 1, 'O')
make_move(board, 0, 1, 'X')
display_board(board)
```

### 14.3 Student Grade Management
```python
import numpy as np

# Students (rows) x Subjects (columns)
# Subjects:  Math, Science, English, History
grades = np.array([
    [85, 92, 88, 90],  # Student 1
    [78, 85, 82, 88],  # Student 2
    [92, 95, 90, 93],  # Student 3
    [88, 85, 87, 86],  # Student 4
    [75, 80, 78, 82]   # Student 5
])

def analyze_grades(grades):
    student_names = ['Alice', 'Bob', 'Charlie', 'David', 'Eve']
    subjects = ['Math', 'Science', 'English', 'History']
    
    # Student averages
    print("Student Averages:")
    student_avgs = np.mean(grades, axis=1)
    for i, name in enumerate(student_names):
        print(f"{name}: {student_avgs[i]:.2f}")
    
    print("\nSubject Averages:")
    subject_avgs = np.mean(grades, axis=0)
    for i, subject in enumerate(subjects):
        print(f"{subject}: {subject_avgs[i]:.2f}")
    
    # Best student
    best_student_idx = np.argmax(student_avgs)
    print(f"\nBest Overall Student: {student_names[best_student_idx]}")
    
    # Hardest subject (lowest average)
    hardest_subject_idx = np.argmin(subject_avgs)
    print(f"Hardest Subject:  {subjects[hardest_subject_idx]} (avg: {subject_avgs[hardest_subject_idx]:.2f})")
    
    # Find students below threshold
    threshold = 85
    print(f"\nStudents with average below {threshold}:")
    for i, avg in enumerate(student_avgs):
        if avg < threshold: 
            print(f"{student_names[i]}: {avg:.2f}")

# Run analysis
analyze_grades(grades)

# Output:
# Student Averages: 
# Alice: 88.75
# Bob: 83.25
# Charlie: 92.50
# David: 86.50
# Eve: 78.75
#
# Subject Averages: 
# Math: 83.60
# Science: 87.40
# English: 85.00
# History: 87.80
#
# Best Overall Student:  Charlie
# Hardest Subject: Math (avg: 83.60)
#
# Students with average below 85:
# Bob: 83.25
# Eve: 78.75
```

### 14.4 Matrix Operations
```python
import numpy as np

# Matrix multiplication example
def matrix_operations():
    # Create two matrices
    matrix_a = np.array([
        [1, 2, 3],
        [4, 5, 6]
    ])
    
    matrix_b = np.array([
        [7, 8],
        [9, 10],
        [11, 12]
    ])
    
    # Matrix multiplication
    result = np. dot(matrix_a, matrix_b)
    print("Matrix A:")
    print(matrix_a)
    print("\nMatrix B:")
    print(matrix_b)
    print("\nA × B:")
    print(result)
    
    # Transpose
    print("\nTranspose of A:")
    print(matrix_a.T)
    
    # Element-wise operations
    matrix_c = np.array([[1, 2], [3, 4]])
    matrix_d = np.array([[5, 6], [7, 8]])
    
    print("\nElement-wise addition:")
    print(matrix_c + matrix_d)
    
    print("\nElement-wise multiplication:")
    print(matrix_c * matrix_d)

matrix_operations()
```

### 14.5 Image Representation (Simplified)
```python
import numpy as np

# Represent a simple 8x8 grayscale image (0=black, 255=white)
def create_simple_image():
    # Create a checkerboard pattern
    image = np.zeros((8, 8), dtype=int)
    
    for i in range(8):
        for j in range(8):
            if (i + j) % 2 == 0:
                image[i][j] = 255
            else:
                image[i][j] = 0
    
    return image

def display_image(image):
    for row in image:
        for pixel in row:
            if pixel == 255:
                print('□', end=' ')
            else:
                print('■', end=' ')
        print()

# Create and display checkerboard
checkerboard = create_simple_image()
print("Checkerboard Pattern:")
display_image(checkerboard)

# Invert image
inverted = 255 - checkerboard
print("\nInverted Pattern:")
display_image(inverted)
```

---

## Summary

### Key Takeaways

1. **Arrays are fundamental data structures** that store elements of the same type in contiguous memory locations. 

2. **Python doesn't have native arrays** - use the `array` module for type-specific arrays or `numpy` for advanced operations.

3. **Time Complexity**:
   - Access: O(1) - Arrays excel at random access
   - Search:  O(N) - Linear search through elements
   - Insert/Delete: O(N) - May require shifting elements
   - Insert/Delete at end: O(1) - Most efficient

4. **Space Complexity**:
   - Most operations: O(1) - Minimal extra space
   - Creating with N elements: O(N) - Must allocate space

5. **When to Use Arrays**:
   - Same data type elements
   - Need fast random access
   - Size is known or stable
   - Memory efficiency matters

6. **When to Avoid Arrays**:
   - Mixed data types needed
   - Frequent insertions/deletions
   - Dynamic size requirements
   - Need flexible structure

7. **Two-Dimensional Arrays**:
   - Essential for matrix operations
   - Used in games, image processing, spreadsheets
   - Most operations are O(M*N)
   - NumPy provides efficient implementations

### Best Practices

1. **Always validate array indices** before accessing to prevent errors
2. **Use NumPy for numerical operations** - it's optimized and feature-rich
3. **Prefer append over insert** when possible (O(1) vs O(N))
4. **Consider the array module** for memory-efficient storage of basic types
5. **Use appropriate data structures** - don't force arrays where lists or other structures fit better

### Next Steps

Now that you've mastered arrays, you're ready to explore: 
- **Lists in Python** - more flexible than arrays
- **Linked Lists** - better for frequent insertions/deletions
- **Stacks and Queues** - specialized array-based structures
- **Hash Tables** - for O(1) lookups with keys
- **Advanced algorithms** - sorting, searching, dynamic programming

---

**End of Guide**

*Remember: Arrays are powerful when used correctly.  Understanding their strengths and limitations will make you a better programmer! *
