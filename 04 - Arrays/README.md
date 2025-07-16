# Comprehensive Guide to Arrays in Python

## 1. Introduction to Arrays

Arrays are fundamental data structures that store elements of the same type in **contiguous memory locations**. Understanding arrays is crucial for efficient programming and data processing.

### Key Properties:
- **Homogeneous elements**: All elements must be of the same data type
- **Contiguous memory allocation**: Elements are stored in adjacent memory locations
- **Zero-based indexing**: First element is at index 0
- **Efficient for numerical data processing**: Direct memory access enables fast operations

### Real-life Analogy
Think of an array like a **macaron box**:
- All slots hold macarons (homogeneous - same type)
- Macarons are tightly packed in order (contiguous memory)
- Each position has a unique identifier (index: 0, 1, 2, ...)
- You can directly access any macaron by its position number

### Exercise 1: Understanding Array Concepts
```python
# Create a simple array to understand the concept
temperatures = [23, 25, 28, 30, 27, 24, 22]
print(f"Temperature on day 3: {temperatures[2]}°C")  # Output: 28°C (index 2)
print(f"First day temperature: {temperatures[0]}°C")  # Output: 23°C
print(f"Last day temperature: {temperatures[-1]}°C")  # Output: 22°C
```

---

## 2. Types of Arrays

### 2.1 One-dimensional Array (1D)
A 1D array is like a single row of elements, accessed using one index.

**Structure**: `[element0, element1, element2, ...]`

#### Example:
```python
# Memory representation: [5, 4, 10, 11, 8, 11, 68, 87, 12]
scores = [5, 4, 10, 11, 8, 11, 68, 87, 12]
print(scores[2])  # Output: 10 (element at index 2)
print(scores[0])  # Output: 5 (first element)
print(scores[8])  # Output: 12 (last element)
```

#### Exercise 2: 1D Array Operations
```python
# Create a 1D array of student grades
grades = [85, 92, 78, 96, 88, 79, 94]

# Access elements
print(f"First student grade: {grades[0]}")
print(f"Third student grade: {grades[2]}")
print(f"Last student grade: {grades[-1]}")

# Calculate average
average = sum(grades) / len(grades)
print(f"Class average: {average:.2f}")
```

### 2.2 Two-dimensional Array (2D)
A 2D array is like a table with rows and columns, accessed using two indices.

**Structure**: `[[row0_col0, row0_col1, ...], [row1_col0, row1_col1, ...], ...]`

#### Example:
```python
# A 3x5 matrix (3 rows, 5 columns)
matrix = [
    [1, 33, 55, 91, 20],  # Row 0
    [5, 4, 10, 11, 8],    # Row 1
    [24, 50, 37, 40, 48]  # Row 2
]

print(matrix[1][2])  # Output: 10 (row 1, column 2)
print(matrix[0][0])  # Output: 1 (top-left element)
print(matrix[2][4])  # Output: 48 (bottom-right element)
```

#### Exercise 3: 2D Array - Student Grades by Subject
```python
# Grades for 3 students in 4 subjects [Math, Science, English, History]
student_grades = [
    [85, 92, 78, 88],  # Student 0
    [90, 85, 95, 82],  # Student 1
    [78, 88, 85, 90]   # Student 2
]

# Access specific grades
print(f"Student 1's Math grade: {student_grades[0][0]}")
print(f"Student 2's English grade: {student_grades[1][2]}")

# Calculate each student's average
for i in range(len(student_grades)):
    avg = sum(student_grades[i]) / len(student_grades[i])
    print(f"Student {i+1} average: {avg:.2f}")
```

### 2.3 Three-dimensional Array (3D)
A 3D array is like a cube with depth, rows, and columns, accessed using three indices.

**Structure**: `[[[depth0_row0_col0, ...], [...]], [[depth1_row0_col0, ...], [...]]]`

#### Example:
```python
# A 3x2x3 cube (3 depth levels, 2 rows, 3 columns each)
cube = [
    [[0, 1, 2], [3, 4, 5]],      # Depth 0
    [[6, 7, 8], [9, 10, 11]],    # Depth 1
    [[12, 13, 14], [15, 16, 17]] # Depth 2
]

print(cube[0][1][2])  # Output: 5 (depth 0, row 1, column 2)
print(cube[1][0][1])  # Output: 7 (depth 1, row 0, column 1)
print(cube[2][1][0])  # Output: 15 (depth 2, row 1, column 0)
```

#### Exercise 4: 3D Array - Sales Data
```python
# Sales data for 2 quarters, 3 months each, 4 products each
# sales[quarter][month][product]
sales = [
    [[100, 150, 200, 120], [110, 160, 210, 130], [120, 170, 220, 140]],  # Q1
    [[130, 180, 230, 150], [140, 190, 240, 160], [150, 200, 250, 170]]   # Q2
]

# Access specific sales data
print(f"Q1 Month 2 Product 3 sales: {sales[0][1][2]}")  # Output: 210
print(f"Q2 Month 1 Product 1 sales: {sales[1][0][0]}")  # Output: 130

# Calculate total sales for Q1
q1_total = sum(sum(month) for month in sales[0])
print(f"Q1 Total Sales: {q1_total}")
```

---

## 3. Arrays in Memory

Understanding how arrays are stored in memory is crucial for optimizing performance.

### Memory Layout Principles:

#### 3.1 One-dimensional Array
- **Storage**: Elements stored sequentially in memory
- **Example**: `[5, 4, 10]` → Memory: `|5|4|10|`

#### 3.2 Two-dimensional Array
- **Storage**: Stored in **row-major order** (rows are flattened consecutively)
- **Example**: `[[1,2,3],[4,5,6]]` → Memory: `|1|2|3|4|5|6|`

#### 3.3 Three-dimensional Array
- **Storage**: Depth layers are flattened row-wise
- **Example**: `[[[0,1],[2,3]], [[4,5],[6,7]]]` → Memory: `|0|1|2|3|4|5|6|7|`

### Key Insight
Multi-dimensional arrays are physically stored as 1D blocks in memory. This contiguous storage enables efficient indexing and memory access patterns.

#### Exercise 5: Memory Layout Understanding
```python
# Visualize memory layout
import numpy as np

# 2D array
arr_2d = np.array([[1, 2, 3], [4, 5, 6]])
print("2D Array:")
print(arr_2d)
print("Flattened (memory layout):")
print(arr_2d.flatten())  # Output: [1 2 3 4 5 6]

# 3D array
arr_3d = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])
print("\n3D Array:")
print(arr_3d)
print("Flattened (memory layout):")
print(arr_3d.flatten())  # Output: [1 2 3 4 5 6 7 8]
```

---

## 4. Creating Arrays in Python

Python provides multiple ways to create arrays, each with specific use cases.

### 4.1 Using `array` Module
The `array` module is efficient for basic numeric types and provides better memory usage than lists.

#### Type Codes:
- `'i'`: signed int
- `'f'`: float
- `'d'`: double
- `'b'`: signed char

#### Examples:
```python
import array

# Empty array of integers
arr_empty = array.array('i')
print(f"Empty array: {arr_empty}")  # Output: array('i')

# Array with elements
arr1 = array.array('i', [1, 2, 3, 4])
print(f"Integer array: {arr1}")  # Output: array('i', [1, 2, 3, 4])

# Array with floats
arr_float = array.array('f', [1.5, 2.7, 3.9])
print(f"Float array: {arr_float}")  # Output: array('f', [1.5, 2.7000000476837158, 3.9000000953674316])
```

#### Exercise 6: Array Module Practice
```python
import array

# Create arrays of different types
int_scores = array.array('i', [85, 92, 78, 96, 88])
float_prices = array.array('f', [19.99, 25.50, 12.75, 8.99])

# Add elements
int_scores.append(94)
float_prices.append(15.25)

print(f"Scores: {int_scores}")
print(f"Prices: {float_prices}")

# Calculate totals
total_score = sum(int_scores)
total_price = sum(float_prices)
print(f"Total score: {total_score}")
print(f"Total price: ${total_price:.2f}")
```

### 4.2 Using `numpy`
NumPy provides powerful tools for multi-dimensional arrays and advanced mathematical operations.

#### Examples:
```python
import numpy as np

# Empty integer array
np_empty = np.array([], dtype=int)
print(f"Empty numpy array: {np_empty}")

# 1D array
np_1d = np.array([1, 2, 3, 4, 5])
print(f"1D array: {np_1d}")

# 2D array
np_2d = np.array([[1, 2], [3, 4]])
print(f"2D array:\n{np_2d}")
print(f"Element at [0][1]: {np_2d[0][1]}")  # Output: 2

# 3D array
np_3d = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])
print(f"3D array:\n{np_3d}")
```

#### Exercise 7: NumPy Array Creation
```python
import numpy as np

# Create arrays using different methods
zeros_array = np.zeros((3, 4))  # 3x4 array of zeros
ones_array = np.ones((2, 3))    # 2x3 array of ones
range_array = np.arange(0, 10, 2)  # [0, 2, 4, 6, 8]
linspace_array = np.linspace(0, 1, 5)  # 5 equally spaced numbers from 0 to 1

print("Zeros array:")
print(zeros_array)
print("\nOnes array:")
print(ones_array)
print(f"\nRange array: {range_array}")
print(f"Linspace array: {linspace_array}")

# Identity matrix
identity = np.eye(3)
print(f"\nIdentity matrix:\n{identity}")
```

### Complexity Analysis:

| Operation | Time | Space |
|-----------|------|-------|
| Create empty array | O(1) | O(1) |
| Create with elements | O(n) | O(n) |

---

## 5. Array Operations

### 5.1 Insertion
Adding elements to an array at different positions has varying time complexities.

#### Types of Insertion:
- **Beginning/Middle**: Requires shifting elements right → O(n)
- **End**: Direct insertion → O(1)

#### Examples:
```python
import array

arr = array.array('i', [1, 2, 3])
print(f"Original array: {arr}")

# Insert at beginning (O(n))
arr.insert(0, 0)
print(f"After insert 0 at beginning: {arr}")

# Insert at middle (O(n))
arr.insert(2, 5)
print(f"After insert 5 at index 2: {arr}")

# Insert at end (O(1)) - using append
arr.append(4)
print(f"After append 4: {arr}")
```

#### Exercise 8: Insertion Operations
```python
import array

# Student IDs array
student_ids = array.array('i', [101, 102, 104, 105])
print(f"Original IDs: {student_ids}")

# New student with ID 103 should be inserted in order
student_ids.insert(2, 103)
print(f"After inserting 103: {student_ids}")

# Add new student at the end
student_ids.append(106)
print(f"After adding 106: {student_ids}")

# Insert multiple students (demonstration)
new_students = [107, 108, 109]
for student_id in new_students:
    student_ids.append(student_id)
print(f"After adding multiple students: {student_ids}")
```

### 5.2 Traversal
Visiting each element in the array sequentially.

#### Time Complexity: O(n)

#### Examples:
```python
import array

def traverse_array(arr):
    """Traverse and print all elements"""
    print("Array elements:")
    for i, element in enumerate(arr):
        print(f"Index {i}: {element}")

# Test traversal
numbers = array.array('i', [10, 20, 30, 40, 50])
traverse_array(numbers)

# Traversal with processing
def sum_array(arr):
    """Calculate sum using traversal"""
    total = 0
    for element in arr:
        total += element
    return total

print(f"Sum of array: {sum_array(numbers)}")
```

#### Exercise 9: Traversal with Conditions
```python
import array

# Find all even numbers in array
def find_even_numbers(arr):
    even_numbers = []
    for element in arr:
        if element % 2 == 0:
            even_numbers.append(element)
    return even_numbers

# Find maximum element
def find_maximum(arr):
    if len(arr) == 0:
        return None
    
    max_element = arr[0]
    for element in arr:
        if element > max_element:
            max_element = element
    return max_element

# Test the functions
test_array = array.array('i', [15, 22, 8, 31, 44, 7, 16])
print(f"Original array: {test_array}")
print(f"Even numbers: {find_even_numbers(test_array)}")
print(f"Maximum element: {find_maximum(test_array)}")
```

### 5.3 Accessing Elements
Direct access to elements using their index.

#### Time Complexity: O(1)

#### Examples:
```python
import array

arr = array.array('i', [10, 20, 30, 40, 50])

# Direct access
print(f"First element: {arr[0]}")      # Output: 10
print(f"Third element: {arr[2]}")      # Output: 30
print(f"Last element: {arr[-1]}")      # Output: 50

# Bounds checking
def safe_access(arr, index):
    """Safely access array element"""
    if 0 <= index < len(arr):
        return arr[index]
    else:
        return f"Index {index} out of bounds"

print(safe_access(arr, 3))   # Output: 40
print(safe_access(arr, 10))  # Output: Index 10 out of bounds
```

#### Exercise 10: Safe Element Access
```python
import array

class SafeArray:
    def __init__(self, type_code, initial_values=None):
        self.array = array.array(type_code, initial_values or [])
    
    def get_element(self, index):
        """Get element with bounds checking"""
        if 0 <= index < len(self.array):
            return self.array[index]
        else:
            raise IndexError(f"Index {index} out of bounds for array of length {len(self.array)}")
    
    def set_element(self, index, value):
        """Set element with bounds checking"""
        if 0 <= index < len(self.array):
            self.array[index] = value
        else:
            raise IndexError(f"Index {index} out of bounds for array of length {len(self.array)}")
    
    def __str__(self):
        return str(self.array)

# Test safe array
safe_arr = SafeArray('i', [1, 2, 3, 4, 5])
print(f"Array: {safe_arr}")

try:
    print(f"Element at index 2: {safe_arr.get_element(2)}")
    safe_arr.set_element(2, 99)
    print(f"After setting index 2 to 99: {safe_arr}")
    
    # This will raise an error
    print(safe_arr.get_element(10))
except IndexError as e:
    print(f"Error: {e}")
```

### 5.4 Searching (Linear Search)
Finding an element in the array by checking each element sequentially.

#### Time Complexity: O(n)
#### Space Complexity: O(1)

#### Examples:
```python
import array

def linear_search(arr, target):
    """Find target element and return its index"""
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1  # Not found

def linear_search_all(arr, target):
    """Find all occurrences of target element"""
    indices = []
    for i in range(len(arr)):
        if arr[i] == target:
            indices.append(i)
    return indices

# Test searching
numbers = array.array('i', [10, 20, 30, 20, 40, 20, 50])
print(f"Array: {numbers}")

print(f"Index of 20: {linear_search(numbers, 20)}")      # Output: 1 (first occurrence)
print(f"Index of 99: {linear_search(numbers, 99)}")      # Output: -1 (not found)
print(f"All indices of 20: {linear_search_all(numbers, 20)}")  # Output: [1, 3, 5]
```

#### Exercise 11: Enhanced Search Functions
```python
import array

def search_with_count(arr, target):
    """Search for target and return index, count, and all positions"""
    indices = []
    for i in range(len(arr)):
        if arr[i] == target:
            indices.append(i)
    
    if indices:
        return {
            'found': True,
            'first_index': indices[0],
            'count': len(indices),
            'all_indices': indices
        }
    else:
        return {
            'found': False,
            'first_index': -1,
            'count': 0,
            'all_indices': []
        }

def search_range(arr, min_val, max_val):
    """Find all elements within a range"""
    result = []
    for i in range(len(arr)):
        if min_val <= arr[i] <= max_val:
            result.append((i, arr[i]))
    return result

# Test enhanced search
test_array = array.array('i', [5, 12, 8, 12, 20, 3, 12, 15])
print(f"Array: {test_array}")

# Search for specific value
search_result = search_with_count(test_array, 12)
print(f"Search for 12: {search_result}")

# Search within range
range_result = search_range(test_array, 10, 20)
print(f"Elements between 10 and 20: {range_result}")
```

### 5.5 Deletion
Removing elements from an array.

#### Types of Deletion:
- **Beginning/Middle**: Requires shifting elements left → O(n)
- **End**: Direct removal → O(1)

#### Examples:
```python
import array

# Deletion by value
arr = array.array('i', [1, 2, 3, 4, 5])
print(f"Original array: {arr}")

arr.remove(3)  # Remove first occurrence of 3
print(f"After removing 3: {arr}")

# Deletion by index
arr = array.array('i', [1, 2, 3, 4, 5])
del arr[1]  # Remove element at index 1
print(f"After deleting index 1: {arr}")

# Pop (remove and return last element)
arr = array.array('i', [1, 2, 3, 4, 5])
last_element = arr.pop()
print(f"Popped element: {last_element}")
print(f"Array after pop: {arr}")
```

#### Exercise 12: Deletion Operations
```python
import array

class ManagedArray:
    def __init__(self, type_code, initial_values=None):
        self.array = array.array(type_code, initial_values or [])
    
    def remove_by_value(self, value):
        """Remove first occurrence of value"""
        try:
            self.array.remove(value)
            return True
        except ValueError:
            return False
    
    def remove_by_index(self, index):
        """Remove element at specific index"""
        if 0 <= index < len(self.array):
            removed = self.array[index]
            del self.array[index]
            return removed
        else:
            raise IndexError(f"Index {index} out of bounds")
    
    def remove_all(self, value):
        """Remove all occurrences of value"""
        count = 0
        while value in self.array:
            self.array.remove(value)
            count += 1
        return count
    
    def __str__(self):
        return str(self.array)
    
    def __len__(self):
        return len(self.array)

# Test managed array
managed = ManagedArray('i', [1, 2, 3, 2, 4, 2, 5])
print(f"Original array: {managed}")

# Remove by value
print(f"Remove 2: {managed.remove_by_value(2)}")
print(f"After removing first 2: {managed}")

# Remove by index
removed = managed.remove_by_index(1)
print(f"Removed element at index 1: {removed}")
print(f"After removing index 1: {managed}")

# Remove all occurrences
count = managed.remove_all(2)
print(f"Removed {count} occurrences of 2")
print(f"Final array: {managed}")
```

---

## 6. Time & Space Complexity Summary

Understanding the performance characteristics of array operations is crucial for writing efficient code.

### Comprehensive Complexity Table:

| Operation | Time Complexity | Space Complexity | Notes |
|-----------|----------------|------------------|-------|
| **Creation** | | | |
| Create empty array | O(1) | O(1) | Constant time initialization |
| Create with n elements | O(n) | O(n) | Must allocate and initialize n elements |
| **Access** | | | |
| Access by index | O(1) | O(1) | Direct memory access |
| **Insertion** | | | |
| Insert at beginning | O(n) | O(1) | Must shift all elements right |
| Insert at middle | O(n) | O(1) | Must shift elements from insertion point |
| Insert at end (append) | O(1) | O(1) | Direct insertion, no shifting needed |
| **Deletion** | | | |
| Delete at beginning | O(n) | O(1) | Must shift all remaining elements left |
| Delete at middle | O(n) | O(1) | Must shift elements from deletion point |
| Delete at end (pop) | O(1) | O(1) | Direct removal, no shifting needed |
| **Search** | | | |
| Linear search | O(n) | O(1) | Must check each element in worst case |
| Binary search (sorted) | O(log n) | O(1) | Only works on sorted arrays |
| **Traversal** | | | |
| Visit all elements | O(n) | O(1) | Must visit each element once |
| **Sorting** | | | |
| Quick sort (average) | O(n log n) | O(log n) | Recursive stack space |
| Merge sort | O(n log n) | O(n) | Additional array for merging |
| Bubble sort | O(n²) | O(1) | Simple but inefficient |

### Performance Implications:

#### Best Case Scenarios:
- **Access**: Always O(1) - arrays excel at random access
- **Insertion/Deletion at end**: O(1) - no element shifting required
- **Search in sorted array**: O(log n) with binary search

#### Worst Case Scenarios:
- **Insertion/Deletion at beginning**: O(n) - maximum element shifting
- **Linear search**: O(n) - element might be at the end or not exist

#### Exercise 13: Performance Comparison
```python
import array
import time

def measure_time(func, *args):
    """Measure execution time of a function"""
    start = time.time()
    result = func(*args)
    end = time.time()
    return result, end - start

def insert_at_beginning(arr, value):
    """Insert value at beginning of array"""
    arr.insert(0, value)

def insert_at_end(arr, value):
    """Insert value at end of array"""
    arr.append(value)

# Create test arrays
small_array = array.array('i', range(1000))
large_array = array.array('i', range(10000))

# Measure insertion at beginning vs end
print("Performance Comparison:")
print("=" * 50)

# Small array
_, time_begin_small = measure_time(insert_at_beginning, small_array.copy(), 999)
_, time_end_small = measure_time(insert_at_end, small_array.copy(), 999)

# Large array
_, time_begin_large = measure_time(insert_at_beginning, large_array.copy(), 999)
_, time_end_large = measure_time(insert_at_end, large_array.copy(), 999)

print(f"Small array (1000 elements):")
print(f"  Insert at beginning: {time_begin_small:.6f} seconds")
print(f"  Insert at end: {time_end_small:.6f} seconds")
print(f"  Ratio: {time_begin_small/time_end_small:.2f}x slower")

print(f"\nLarge array (10000 elements):")
print(f"  Insert at beginning: {time_begin_large:.6f} seconds")
print(f"  Insert at end: {time_end_large:.6f} seconds")
print(f"  Ratio: {time_begin_large/time_end_large:.2f}x slower")
```

### Memory Usage Considerations:

#### Space Efficiency:
- **Arrays**: More memory efficient than lists for homogeneous data
- **Contiguous allocation**: Better cache performance
- **No pointer overhead**: Each element stores actual value, not reference

#### Exercise 14: Memory Usage Comparison
```python
import array
import sys

# Compare memory usage of different data structures
def compare_memory_usage():
    n = 1000
    
    # Python list
    python_list = list(range(n))
    
    # Array module
    array_int = array.array('i', range(n))
    
    # Calculate memory usage
    list_memory = sys.getsizeof(python_list) + sum(sys.getsizeof(x) for x in python_list)
    array_memory = sys.getsizeof(array_int) + array_int.buffer_info()[1] * array_int.itemsize
    
    print(f"Memory Usage Comparison for {n} integers:")
    print(f"Python list: {list_memory} bytes")
    print(f"Array module: {array_memory} bytes")
    print(f"Space savings: {((list_memory - array_memory) / list_memory) * 100:.1f}%")

compare_memory_usage()
```

---

## Conclusion

Arrays are fundamental data structures that provide efficient storage and access patterns for homogeneous data. Key takeaways:

1. **Choose the right type**: Use `array` module for memory efficiency, `numpy` for mathematical operations
2. **Consider access patterns**: Arrays excel at random access (O(1)) but struggle with insertions/deletions in the middle (O(n))
3. **Memory matters**: Contiguous storage provides better cache performance than scattered data structures
4. **Understand complexity**: Know when operations are expensive (O(n)) vs cheap (O(1))

Arrays form the foundation for more complex data structures and algorithms, making them essential for any programmer to master.
