# Complete Big O Notation Guide

## Table of Contents
1. [Introduction to Big O](#introduction-to-big-o)
2. [Big O Worst Case](#big-o-worst-case)
3. [O(n) - Linear Time](#on---linear-time)
4. [Drop Constants Rule](#drop-constants-rule)
5. [O(n²) - Quadratic Time](#on²---quadratic-time)
6. [Drop Non-Dominants Rule](#drop-non-dominants-rule)
7. [O(1) - Constant Time](#o1---constant-time)
8. [O(log n) - Logarithmic Time](#olog-n---logarithmic-time)
9. [Different Terms for Inputs](#different-terms-for-inputs)
10. [Big O of Lists](#big-o-of-lists)
11. [5 Rules Summary](#5-rules-summary)

---

## Introduction to Big O

Big O notation is a mathematical way to compare the efficiency of different algorithms. It measures how code performs as the input size grows.

### Key Concepts:
- **Time Complexity**: How execution time changes with input size
- **Space Complexity**: How memory usage changes with input size
- **Not measured in actual time**: Measured in number of operations
- **Primary focus**: Time complexity (space complexity is also important)

### Why Big O Matters:
- Critical for coding interviews
- Helps choose the most efficient algorithm
- Predicts performance with large datasets

---

## Big O Worst Case

Big O uses three Greek letters to describe different scenarios:

| Symbol | Name | Scenario | Big O Equivalent |
|--------|------|----------|------------------|
| Ω (Omega) | Best Case | Finding item on first try | Not called "Big O" |
| Θ (Theta) | Average Case | Finding item in middle | Not called "Big O" |
| O (Omicron) | Worst Case | Finding item at end | **This is Big O** |

### Example: Searching in a list [1, 2, 3, 4, 5, 6, 7]
- **Best case (Ω)**: Looking for 1 → Found in 1 operation
- **Average case (Θ)**: Looking for 4 → Found in ~3.5 operations
- **Worst case (O)**: Looking for 7 → Found in 7 operations

**Important**: Big O always refers to worst-case scenario.

---

## O(n) - Linear Time

### Code Example:
```python
def print_items(n):
    for i in range(n):
        print(i)

print_items(10)
```

**Output**: 0, 1, 2, 3, 4, 5, 6, 7, 8, 9

### Analysis:
- **Input**: n = 10
- **Operations**: 10 print statements
- **Big O**: O(n) because operations scale linearly with input

### Characteristics:
- **Proportional**: As n doubles, operations double
- **Graph**: Straight line
- **Common in**: Single loops, linear searches

---

## Drop Constants Rule

### Code Example:
```python
def print_items(n):
    for i in range(n):
        print(i)
    
    for j in range(n):
        print(j)

print_items(10)
```

**Output**: 0-9 (first loop), then 0-9 (second loop) = 20 items total

### Analysis:
- **Operations**: n + n = 2n
- **Before simplification**: O(2n)
- **After dropping constant**: O(n)

### Rule:
Drop constants from Big O notation:
- O(2n) → O(n)
- O(10n) → O(n)
- O(100n) → O(n)

---

## O(n²) - Quadratic Time

### Code Example:
```python
def print_items(n):
    for i in range(n):
        for j in range(n):
            print(i, j)

print_items(10)
```

**Output**: (0,0), (0,1), ..., (9,9) = 100 pairs total

### Analysis:
- **Nested loops**: Outer loop runs n times, inner loop runs n times for each outer iteration
- **Total operations**: n × n = n²
- **Big O**: O(n²)

### Characteristics:
- **Much less efficient** than O(n)
- **Graph**: Steep curve
- **Common in**: Nested loops, bubble sort

---

## Drop Non-Dominants Rule

### Code Example:
```python
def print_items(n):
    for i in range(n):
        for j in range(n):
            print(i, j)
    
    for k in range(n):
        print(k)

print_items(10)
```

**Output**: 100 pairs (from nested loops) + 10 single values = 110 items total

### Analysis:
- **Nested loops**: O(n²) operations
- **Single loop**: O(n) operations
- **Total**: O(n² + n)
- **Simplified**: O(n²) - we drop the non-dominant term

### Rule:
When you have multiple terms, keep only the dominant (fastest-growing) term:
- O(n² + n) → O(n²)
- O(n³ + n² + n) → O(n³)

### Why we drop non-dominants:
For large n, the dominant term overwhelms others:
- n = 100: n² = 10,000 vs n = 100 (n is only 1% of total)
- n = 1,000: n² = 1,000,000 vs n = 1,000 (n is only 0.1% of total)

---

## O(1) - Constant Time

### Code Example:
```python
def add_items(n):
    return n + n + n

print(add_items(10))
```

**Output**: 30

### Analysis:
- **Operations**: 2 additions (regardless of n value)
- **Big O**: O(1)

### Characteristics:
- **Most efficient** Big O possible
- **Same performance** whether n = 1 or n = 1,000,000
- **Also called**: Constant time
- **Graph**: Flat horizontal line

### Examples of O(1) operations:
- Mathematical calculations
- Array access by index
- Adding/removing from end of array

---

## O(log n) - Logarithmic Time

### Binary Search Example:
Searching for 1 in sorted array [1, 2, 3, 4, 5, 6, 7, 8]:

**Step 1**: Check middle (between 4 and 5)
- 1 < 4, so eliminate right half: [1, 2, 3, 4]

**Step 2**: Check middle (between 2 and 3)
- 1 < 2, so eliminate right half: [1, 2]

**Step 3**: Check middle (1)
- Found! 1 = 1

### Analysis:
- **List size**: 8 items
- **Steps needed**: 3 steps
- **Mathematical relationship**: 2³ = 8, so log₂(8) = 3

### The Power of O(log n):
For a list with 1,073,741,824 items (over 1 billion):
- **Linear search O(n)**: Up to 1 billion operations
- **Binary search O(log n)**: Only 31 operations!

### Characteristics:
- **Very efficient** (second only to O(1))
- **Requires sorted data** for binary search
- **Graph**: Gradually flattening curve
- **Common in**: Binary search, balanced tree operations

---

## Different Terms for Inputs

This is a common interview "gotcha" question.

### Single Parameter Example:
```python
def print_items(n):
    for i in range(n):
        print(i)
    
    for j in range(n):
        print(j)

print_items(10)
```
**Big O**: O(n) (we can drop constants)

### Two Parameters Example:
```python
def print_items(a, b):
    for i in range(a):
        print(i)
    
    for j in range(b):
        print(j)

print_items(1, 10)
```
**Big O**: O(a + b) (cannot simplify further)

### Nested Loops with Different Parameters:
```python
def print_items(a, b):
    for i in range(a):
        for j in range(b):
            print(i, j)

print_items(3, 5)
```
**Big O**: O(a × b)

### Key Rule:
You cannot assume different parameters are equal. Each parameter represents a different input size.

---

## Big O of Lists

Understanding list operations is crucial since lists are fundamental data structures.

### List Operations Analysis:

| Operation | Big O | Explanation |
|-----------|-------|-------------|
| `append()` | O(1) | Add to end, no re-indexing needed |
| `pop()` | O(1) | Remove from end, no re-indexing needed |
| `pop(0)` | O(n) | Remove from beginning, re-index all items |
| `insert(0, val)` | O(n) | Insert at beginning, re-index all items |
| `insert(i, val)` | O(n) | Insert at middle, re-index remaining items |
| `remove(val)` | O(n) | Search for value, then remove |
| `list[i]` | O(1) | Access by index, direct memory access |

### Visual Example:
```
Original list: [11, 3, 23, 7]
Indexes:       [0,  1, 2,  3]
```

#### Efficient Operations O(1):
```python
my_list.append(17)    # [11, 3, 23, 7, 17]
my_list.pop()         # [11, 3, 23, 7]
value = my_list[2]    # Access index 2 → returns 23
```

#### Inefficient Operations O(n):
```python
my_list.pop(0)        # Remove first item
# Result: [3, 23, 7]
# Indexes: [0, 1, 2]  ← All items re-indexed!

my_list.insert(0, 11) # Insert at beginning
# Result: [11, 3, 23, 7]
# Indexes: [0, 1, 2, 3]  ← All items re-indexed!
```

### Why Re-indexing is Expensive:
When you remove or insert at the beginning or middle of a list, all subsequent elements must be shifted, requiring O(n) operations.

---

## 5 Rules Summary

Here are the fundamental rules for measuring Big O complexity:

### Rule 1: Simple Operations = O(1)
Any assignment statements and if statements executed once regardless of problem size.
```python
x = 5        # O(1)
if x > 0:    # O(1)
    y = 10   # O(1)
```

### Rule 2: Simple For Loop = O(n)
A simple "for" loop from 0 to n (with no internal loops).
```python
for i in range(n):  # O(n)
    print(i)
```

### Rule 3: Nested Loop = O(n²)
A nested loop of the same type takes quadratic time complexity.
```python
for i in range(n):      # O(n²)
    for j in range(n):
        print(i, j)
```

### Rule 4: Divide by Two = O(log n)
A loop where the controlling parameter is divided by two at each step.
```python
while n > 1:    # O(log n)
    n = n // 2
```

### Rule 5: Multiple Statements = Add Them Up
When dealing with multiple statements, add their complexities.
```python
# O(n) + O(n²) + O(1) = O(n²)
for i in range(n):          # O(n)
    print(i)

for i in range(n):          # O(n²)
    for j in range(n):
        print(i, j)

x = 5                       # O(1)
```

---

## Big O Efficiency Ranking

From most efficient to least efficient:

1. **O(1)** - Constant time
2. **O(log n)** - Logarithmic time
3. **O(n)** - Linear time
4. **O(n log n)** - Linearithmic time (efficient sorting algorithms)
5. **O(n²)** - Quadratic time
6. **O(n³)** - Cubic time
7. **O(2ⁿ)** - Exponential time

### Key Takeaways:
- Always strive for O(1) when possible
- O(log n) is excellent for search operations
- O(n) is acceptable for most operations
- O(n²) and worse should be avoided for large datasets
- Understanding these complexities is essential for technical interviews and efficient programming
