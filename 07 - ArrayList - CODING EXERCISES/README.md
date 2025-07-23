# Array/List Interview Questions Guide

## Table of Contents
1. [Question 1: Finding Missing Number](#question-1-finding-missing-number)
2. [Question 2: Two Sum Problem (Pairs)](#question-2-two-sum-problem-pairs)
3. [Question 3: Finding a Number in Array](#question-3-finding-a-number-in-array)
4. [Question 4: Permutation Check](#question-4-permutation-check)

---

## Question 1: Finding Missing Number

### Problem Statement
Find the missing element in an array of integers that contains numbers between 1 and 100, where one number is missing.

### Key Concept
This problem is frequently asked at major tech companies like Google, Amazon, Facebook, and Microsoft during campus interviews.

### Solution Approach
**Mathematical Trick**: Use the sum of n series equation:
```
Sum = n × (n + 1) / 2
```

### Algorithm Steps
1. Calculate the expected sum of numbers from 1 to n using the formula
2. Calculate the actual sum of numbers in the given array
3. The difference between these sums is the missing number

### Python Implementation
```python
def findMissing(my_list, n):
    # Calculate sum of numbers from 1 to n
    sum1 = n * (n + 1) // 2
    
    # Calculate sum of numbers in the list
    sum2 = sum(my_list)
    
    # Missing number is the difference
    missing_number = sum1 - sum2
    return missing_number

# Example usage
# If we have a list from 1 to 100 with one missing number
my_list = [1, 2, 3, ..., 72, 74, ..., 100]  # 73 is missing
result = findMissing(my_list, 100)
print(result)  # Output: 73
```

### Time Complexity
- O(n) for calculating the sum of the list
- Very efficient and optimal solution

---

## Question 2: Two Sum Problem (Pairs)

### Problem Statement
Write a program to find all pairs of integers whose sum is equal to a given number.

This is equivalent to LeetCode Problem #1 (Two Sum), where given an array of integers and a target, return the indices of two numbers that add up to the target.

### Example
- Input array: [2, 7, 11, 15], Target: 9
- Output: [0, 1] (because array[0] + array[1] = 2 + 7 = 9)

### Important Interview Questions to Ask
Before coding, always clarify these points:
1. Does the array contain only positive or negative numbers?
2. What if the same pair repeats twice?
3. Is the reverse of a pair acceptable? (e.g., both [4,1] and [1,4] for sum=5)
4. Do we need only distinct pairs?
5. How big is the array?

### Solution Implementation
```python
def find_pairs(nums, target):
    """
    Find all pairs with distinct elements that sum to target
    """
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            # Skip if pairs are equal (for distinct pairs requirement)
            if nums[i] == nums[j]:
                continue
            elif nums[i] + nums[j] == target:
                print(f"Indices: {i} and {j}")
                print(f"Values: {nums[i]} and {nums[j]}")

# Example usage
my_list = [1, 2, 3, 2, 3, 4, 5, 4]
find_pairs(my_list, 6)

# Output:
# Indices: 0 and 6 (values: 1 and 5)
# Indices: 1 and 5 (values: 2 and 4)
# Indices: 3 and 7 (values: 2 and 4)
# Note: [3,3] pairs are skipped due to distinct requirement
```

### Time Complexity
- O(n²) with nested loops
- Can be optimized to O(n) using hash maps for single pair solutions

---

## Question 3: Finding a Number in Array

### Problem Statement
Test if an array contains a certain value. Write a method to search for an element in an array using algorithms (not built-in methods).

### Key Points
- Many programming languages don't have built-in search methods for arrays
- Python lists have the `in` operator, but interviewers often want algorithmic solutions
- We'll implement using NumPy arrays and linear search

### Linear Search Implementation
```python
import numpy as np

def find_number(array, number):
    """
    Linear search to find a number in array
    Returns the index if found, nothing if not found
    """
    for i in range(len(array)):
        if array[i] == number:
            print(f"Found at index: {i}")
            return i
    
    # Optional: handle case when not found
    print("Element not found")
    return -1

# Example usage
myArray = np.array([1, 4, 7, 9, 11, 13, 15, 17, 19, 21, 23, 25])

# Search for existing element
find_number(myArray, 13)  # Output: Found at index: 5

# Search for non-existing element  
find_number(myArray, 12)  # Output: Element not found
```

### Enhanced Version with Better Error Handling
```python
def find_number_enhanced(array, number):
    for i in range(len(array)):
        if array[i] == number:
            return f"Element {number} found at index {i}"
    return f"Element {number} not found in the array"
```

### Time Complexity
- O(n) in worst case (when element is at the end or not present)
- O(1) in best case (when element is at the beginning)

---

## Question 4: Permutation Check

### Problem Statement
Given two lists, write a method to decide if one is a permutation of another.

### Definition of Permutation
Two lists are permutations if they have the same elements but in different orders.

**String Examples:**
- "peek" and "keep" ✓
- "rail" and "lair" ✓

### Solution Strategy
Use the sort function to compare lists after sorting.

### Algorithm Steps
1. Check if both lists have the same length
2. If lengths differ, return False
3. Sort both lists
4. Compare sorted lists for equality

### Python Implementation
```python
def permutation(list1, list2):
    """
    Check if two lists are permutations of each other
    """
    # Check if lengths are different
    if len(list1) != len(list2):
        return False
    
    # Sort both lists (modifies original lists)
    list1.sort()
    list2.sort()
    
    # Compare sorted lists
    if list1 == list2:
        return True
    else:
        return False

# Example 1: Integer lists
list1 = [1, 2, 3]
list2 = [1, 3, 2]
result = permutation(list1, list2)
print(result)  # Output: True

# Example 2: String character lists
list1 = ['a', 'c', 'b']
list2 = ['c', 'a', 'b']
result = permutation(list1, list2)
print(result)  # Output: True

# Example 3: Non-permutation
list1 = ['a', 'c', 'b']
list2 = ['c', 'a', 'd']  # 'd' is different
result = permutation(list1, list2)
print(result)  # Output: False
```

### Alternative Implementation (Preserving Original Lists)
```python
def permutation_safe(list1, list2):
    """
    Check permutation without modifying original lists
    """
    if len(list1) != len(list2):
        return False
    
    # Create copies to avoid modifying originals
    sorted_list1 = sorted(list1)
    sorted_list2 = sorted(list2)
    
    return sorted_list1 == sorted_list2
```

### Time Complexity
- O(n log n) due to sorting operations
- Space complexity: O(1) if modifying original lists, O(n) if creating copies

---

## Summary

These four questions cover fundamental array manipulation concepts commonly tested in technical interviews:

1. **Missing Number**: Mathematical approach using sum formulas
2. **Two Sum**: Nested loop approach with consideration for edge cases
3. **Linear Search**: Basic searching algorithm implementation
4. **Permutation Check**: Using sorting to compare list contents

### Interview Tips
1. **Always ask clarifying questions** before coding
2. **Consider edge cases** (empty arrays, duplicates, etc.)
3. **Discuss time and space complexity**
4. **Test your solution** with examples
5. **Think about optimization** opportunities

These problems demonstrate essential problem-solving skills and algorithmic thinking that interviewers look for in candidates.
