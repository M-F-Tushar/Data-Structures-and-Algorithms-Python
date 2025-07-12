# Big O Interview Questions - Complete Guide

## Overview
This guide covers the top 10 Big O interview questions commonly asked at major tech companies like Facebook, Amazon, Apple, and Microsoft. Each question includes detailed analysis, step-by-step solutions, and practical examples.

---

## Question 1: Sequential Operations

### Problem
Find the runtime complexity of the following code:

```python
def foo(array):
    sum = 0
    product = 1
    for i in array:
        sum += i
    for i in array:
        product *= i
    print("Sum = "+str(sum)+", Product = "+str(product))
```

### Analysis
Let's break down each operation:

1. **Line 2**: `sum = 0` → **O(1)** - constant time assignment
2. **Line 3**: `product = 1` → **O(1)** - constant time assignment
3. **Line 4-5**: First loop through array → **O(n)** - linear time
4. **Line 6-7**: Second loop through array → **O(n)** - linear time
5. **Line 8**: Print statement → **O(1)** - constant time

### Solution
- Total: O(1) + O(1) + O(n) + O(n) + O(1)
- Simplified: O(n) + O(n) = O(2n)
- **Final Answer: O(n)**

**Key Insight**: The fact that we iterate through the array twice doesn't change the complexity from linear to quadratic. We drop constants, so O(2n) becomes O(n).

---

## Question 2: Nested Loops (Same Array)

### Problem
Find the runtime complexity of the following code:

```python
def printPairs(array):
    for i in array:
        for j in array:
            print(str(i)+","+str(j))
```

### Analysis
- **Outer loop**: Runs n times (where n = length of array)
- **Inner loop**: For each outer loop iteration, runs n times
- **Print statement**: O(1) constant time operation

### Solution
- Inner loop: O(n) iterations
- Outer loop: O(n) iterations
- Total: O(n) × O(n) = **O(n²)**

**Key Insight**: When you have nested loops iterating over the same array, the time complexity is quadratic. This code prints all possible pairs from the array, resulting in n² pairs.

---

## Question 3: Nested Loops (Avoiding Duplicates)

### Problem
Find the runtime complexity of the following code:

```python
def printUnorderedPairs(array):
    for i in range(0, len(array)):
        for j in range(i+1, len(array)):
            print(array[i] + "," + array[j])
```

### Analysis
This is trickier because the inner loop doesn't always run n times.

#### Method 1: Counting Iterations
- **First iteration**: Inner loop runs (n-1) times
- **Second iteration**: Inner loop runs (n-2) times
- **Third iteration**: Inner loop runs (n-3) times
- **...continues until**: Inner loop runs 1 time

Total iterations: (n-1) + (n-2) + (n-3) + ... + 1

This is the sum of integers from 1 to (n-1):
- Formula: n(n-1)/2
- Simplified: (n² - n)/2
- **Final Answer: O(n²)** (dropping constants and non-dominant terms)

#### Method 2: Average Work
- **Outer loop**: Runs n times
- **Inner loop**: Average iterations = n/2
- **Total**: n × (n/2) = n²/2 = **O(n²)**

### Solution
Both methods confirm: **O(n²)**

---

## Question 4: Nested Loops (Different Arrays)

### Problem
Find the runtime complexity of the following code:

```python
def printUnorderedPairs(arrayA, arrayB):
    for i in range(len(arrayA)):
        for j in range(len(arrayB)):
            if arrayA[i] < arrayB[j]:
                print(str(arrayA[i]) + "," + str(arrayB[j]))
```

### Analysis
- **If condition**: O(1) - constant time operation
- **Outer loop**: Runs 'a' times (where a = length of arrayA)
- **Inner loop**: Runs 'b' times (where b = length of arrayB)

### Solution
**Answer: O(a × b)**

**Common Mistake**: Many students think this should be O(n²), but that's incorrect! Since we're dealing with two different arrays, the complexity depends on both array sizes.

**Key Insight**: Only when both loops iterate over the same array does the complexity become O(n²).

---

## Question 5: Nested Loops with Constant Inner Loop

### Problem
Find the runtime complexity of the following code:

```python
def printUnorderedPairs(arrayA, arrayB):
    for i in range(len(arrayA)):
        for j in range(len(arrayB)):
            for k in range(0, 100000):
                print(str(arrayA[i]) + "," + str(arrayB[j]))
```

### Analysis
- **First two loops**: O(a × b) (from previous question)
- **Third loop**: Runs 100,000 times - this is a constant!
- **Print statement**: O(1)

### Solution
- Total: O(a × b × 100000)
- Since 100,000 is constant: **O(a × b)**

**Key Insight**: Constants don't affect Big O complexity. Whether the inner loop runs 10 times or 100,000 times, it's still O(1).

---

## Question 6: Array Reversal

### Problem
Find the runtime complexity of the following code:

```python
def reverse(array):
    for i in range(0, int(len(array)/2)):
        other = len(array) - i - 1
        temp = array[i]
        array[i] = array[other]
        array[other] = temp
    print(array)
```

### Analysis
Step by step:
1. **Loop**: Runs n/2 times → O(n/2) → O(n)
2. **Line 3**: Variable assignment → O(1)
3. **Line 4**: Array access → O(1)
4. **Line 5**: Array assignment → O(1)
5. **Line 6**: Array assignment → O(1)
6. **Line 7**: Print array → O(1)

### Solution
- Total: O(n) + O(1) + O(1) + O(1) + O(1) + O(1)
- **Final Answer: O(n)**

**Key Insight**: Even though we only iterate through half the array, O(n/2) simplifies to O(n) after dropping constants.

---

## Question 7: Identifying Equivalent Complexities

### Problem
Which of the following are equivalent to O(n)?

1. O(n + p), where p < n/2
2. O(2n)
3. O(n + log n)
4. O(n + n log n)
5. O(n + m)

### Analysis
Use the Big O complexity hierarchy graph to identify dominant terms:

**Complexity Hierarchy** (fastest to slowest):
O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ)

### Solutions

1. **O(n + p), where p < n/2**: 
   - Since p < n/2, n is the dominant term
   - Drop p → **O(n) ✓**

2. **O(2n)**:
   - Drop constant 2 → **O(n) ✓**

3. **O(n + log n)**:
   - n is dominant over log n
   - Drop log n → **O(n) ✓**

4. **O(n + n log n)**:
   - n log n is dominant over n
   - Drop n → **O(n log n) ✗**

5. **O(n + m)**:
   - No relationship established between n and m
   - Cannot drop either → **O(n + m) ✗**

**Answer**: Options 1, 2, and 3 are equivalent to O(n).

---

## Question 8: Factorial Recursion

### Problem
Find the runtime complexity of the following recursive factorial function:

```python
def factorial(n):
    if n < 0:
        return -1
    elif n == 0:
        return 1
    else:
        return n * factorial(n-1)
```

### Analysis
For recursive functions, we use the recurrence relation method:

Let T(n) = time complexity of factorial(n)

**Recurrence Relation:**
- T(n) = T(n-1) + O(1)
- T(0) = O(1)

**Expansion:**
- T(n) = T(n-1) + 1
- T(n-1) = T(n-2) + 1
- T(n-2) = T(n-3) + 1
- ...
- T(1) = T(0) + 1 = 1 + 1 = 2

**Total Steps:**
T(n) = T(0) + n = 1 + n = n + 1

### Solution
**Answer: O(n)**

**Key Insight**: The function calls itself n times, each with constant work, resulting in linear complexity.

---

## Question 9: Fibonacci Recursion

### Problem
Find the runtime complexity of the following code:

```python
def allFib(n):
    for i in range(n):
        print(str(i) + ":, " + str(fib(i)))

def fib(n):
    if n <= 0:
        return 0
    elif n == 1:
        return 1
    return fib(n-1) + fib(n-2)
```

### Analysis

#### Step 1: Analyze fib(n)
The fib function makes 2 recursive calls, creating a binary tree of calls.
- **Branches**: 2 (each call makes 2 more calls)
- **Depth**: n (parameter decreases by 1 each time)
- **Complexity**: O(2ⁿ)

#### Step 2: Analyze allFib(n)
- Calls fib(0): ~2⁰ operations
- Calls fib(1): ~2¹ operations  
- Calls fib(2): ~2² operations
- ...
- Calls fib(n): ~2ⁿ operations

**Total work**: 2⁰ + 2¹ + 2² + ... + 2ⁿ

**Sum of powers of 2**: 2^(n+1) - 1

### Solution
**Answer: O(2ⁿ)**

**Key Insight**: Even though we call fib() n times, the exponential growth of each call dominates, making the overall complexity exponential.

---

## Question 10: Powers of Two

### Problem
Find the runtime complexity of the following function that prints powers of 2:

```python
def powersOf2(n):
    if n < 1:
        return 0
    elif n == 1:
        print(1)
        return 1
    else:
        prev = powersOf2(int(n/2))
        print(prev)
        curr = prev * 2
        print(curr)
        return curr
```

### Analysis
Let's trace through the execution for n = 50:

1. **powersOf2(50)** calls **powersOf2(25)**
2. **powersOf2(25)** calls **powersOf2(12)**
3. **powersOf2(12)** calls **powersOf2(6)**
4. **powersOf2(6)** calls **powersOf2(3)**
5. **powersOf2(3)** calls **powersOf2(1)**
6. **powersOf2(1)** returns 1

**Pattern**: Each call divides n by 2 until we reach 1.

**Number of divisions**: log₂(n)

### Solution
**Answer: O(log n)**

**Key Insight**: Any algorithm that repeatedly divides the problem size by 2 (or any constant) until reaching 1 has logarithmic complexity.

---

## Summary of Key Concepts

### 1. **Drop Constants and Non-Dominant Terms**
- O(2n) → O(n)
- O(n² + n) → O(n²)
- O(n + log n) → O(n)

### 2. **Nested Loops Rules**
- Same array: O(n²)
- Different arrays: O(a × b)
- Constant inner loop: doesn't change complexity

### 3. **Recursive Complexity**
- **Single recursion**: Usually O(n)
- **Binary recursion**: Usually O(2ⁿ)
- **Divide by 2**: Usually O(log n)

### 4. **Common Complexity Hierarchy**
O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ)

### 5. **Analysis Tips**
- Count the number of times each operation executes
- For recursion, set up recurrence relations
- Use the complexity hierarchy to identify dominant terms
- Always consider the worst-case scenario

---

## Practice Strategy

1. **Start with the basics**: Understand single loops, nested loops, and simple recursion
2. **Master the rules**: Memorize common patterns but understand why they work
3. **Practice tracing**: Walk through code execution step by step
4. **Use visual aids**: Draw recursion trees for complex recursive functions
5. **Time yourself**: Practice solving these under interview conditions

Remember: Big O analysis is about understanding the growth rate of algorithms as input size increases. Focus on the dominant operations and ignore constants and lower-order terms.
