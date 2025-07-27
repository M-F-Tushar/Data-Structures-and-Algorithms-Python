# Complete Linked List Data Structure Guide

## Table of Contents
1. [Introduction to Linked Lists](#introduction-to-linked-lists)
2. [Big O Analysis](#big-o-analysis)
3. [Under the Hood Implementation](#under-the-hood-implementation)
4. [Constructor and Node Class](#constructor-and-node-class)
5. [Print List Method](#print-list-method)
6. [Core Methods Implementation](#core-methods-implementation)
7. [Advanced Operations](#advanced-operations)
8. [Practice Exercises](#practice-exercises)

---

## 1. Introduction to Linked Lists

### What is a Linked List?

A **Linked List** is a linear data structure where elements (called nodes) are stored in sequence, but unlike arrays/lists, they are not stored in contiguous memory locations.

### Key Differences from Regular Lists

| Feature | Regular List (Array) | Linked List |
|---------|---------------------|-------------|
| **Memory Layout** | Contiguous (elements next to each other) | Non-contiguous (spread throughout memory) |
| **Indexing** | Has indexes (0, 1, 2, ...) | No indexes |
| **Access Method** | Direct access via index O(1) | Sequential traversal O(n) |
| **Visual Representation** | Green squares ■■■■ | Purple circles ●→●→●→● |

### Structure Components

```
HEAD → ●(11) → ●(3) → ●(23) → ●(7) → None
       ↑                            ↑
    First Node                  TAIL points here
```

- **HEAD**: Points to the first node in the list
- **TAIL**: Points to the last node in the list  
- **Node**: Contains both data (value) and a pointer to the next node
- **Next Pointer**: Links one node to the next
- **None**: The last node points to None (end of list)

### Memory Visualization

**Regular List in Memory:**
```
Memory: [11][3][23][7] - All consecutive
Index:   0   1   2   3  - Direct access
```

**Linked List in Memory:**
```
Memory: [7]...[11]...[23]...[3] - Scattered locations
Links:  HEAD→11→3→23→7→None     - Connected by pointers
```

---

## 2. Big O Analysis

### Time Complexity Comparison

| Operation | Linked List | Regular List |
|-----------|-------------|--------------|
| **Append (end)** | O(1) | O(1) |
| **Prepend (beginning)** | O(1) | O(n) |
| **Pop (end)** | O(n) | O(1) |
| **Pop First (beginning)** | O(1) | O(n) |
| **Insert (middle)** | O(n) | O(n) |
| **Remove (middle)** | O(n) | O(n) |
| **Lookup by value** | O(n) | O(n) |
| **Lookup by index** | O(n) | O(1) |

### Detailed Analysis

#### Append - O(1)
```
Before: HEAD → ●(11) → ●(3) → ●(7) → None
                              ↑
                            TAIL

After:  HEAD → ●(11) → ●(3) → ●(7) → ●(4) → None
                                     ↑
                                   TAIL
```
**Why O(1)?** We have direct access to the tail, so adding is constant time regardless of list size.

#### Pop (from end) - O(n)
```
Before: HEAD → ●(11) → ●(3) → ●(7) → None
                              ↑
                            TAIL

After:  HEAD → ●(11) → ●(3) → None
                        ↑
                      TAIL
```
**Why O(n)?** To move TAIL to the second-to-last node, we must traverse from HEAD because we can't go backwards.

#### Prepend - O(1)
```
Before: HEAD → ●(11) → ●(3) → ●(7) → None

After:  HEAD → ●(4) → ●(11) → ●(3) → ●(7) → None
```
**Why O(1)?** We directly access HEAD and update pointers in constant time.

#### Pop First - O(1)
```
Before: HEAD → ●(11) → ●(3) → ●(7) → None

After:         HEAD → ●(3) → ●(7) → None
```
**Why O(1)?** We move HEAD to the next node in constant time.

---

## 3. Under the Hood Implementation

### Node Structure Concept

Each node is essentially like a dictionary:
```python
# Conceptual representation (not actual syntax)
node = {
    "value": 4,
    "next": pointer_to_next_node
}
```

### Real Implementation Example

```python
# Creating a linked list structure with nested dictionaries
head = {
    "value": 11,
    "next": {
        "value": 3, 
        "next": {
            "value": 23,
            "next": {
                "value": 7,
                "next": None
            }
        }
    }
}

# Accessing the value 23 (third node)
print(head["next"]["next"]["value"])  # Output: 23
```

### Actual Linked List Syntax
```python
# With proper linked list implementation
print(my_linked_list.head.next.next.value)  # Output: 23
```

The syntax is very similar - you traverse through `.next` pointers to reach the desired node.

---

## 4. Constructor and Node Class

### Node Class Implementation

```python
class Node:
    def __init__(self, value):
        self.value = value  # Store the data
        self.next = None    # Initially points to nothing
```

**What the Node class does:**
- Creates individual nodes for the linked list
- Each node contains a value and a next pointer
- Used by all methods that need to create new nodes (constructor, append, prepend, insert)

### LinkedList Class Implementation

```python
class LinkedList:
    def __init__(self, value):
        # Create the first node
        new_node = Node(value)
        
        # Set head and tail to point to this first node
        self.head = new_node
        self.tail = new_node
        
        # Initialize length
        self.length = 1
```

### Creating a Linked List Example

```python
# Create a new linked list with initial value 4
my_linked_list = LinkedList(4)

# This creates:
# HEAD → ●(4) → None
#        ↑
#      TAIL

# Access the value
print(my_linked_list.head.value)  # Output: 4
```

**What happens when you create `LinkedList(4)`:**
1. Calls `Node(4)` to create a new node with value 4
2. Sets both `head` and `tail` to point to this node
3. Sets `length` to 1
4. Returns the linked list object

---

## 5. Print List Method

### Implementation

```python
def print_list(self):
    temp = self.head
    while temp is not None:
        print(temp.value)
        temp = temp.next
```

### Step-by-Step Execution

```python
# Given: HEAD → ●(11) → ●(3) → ●(23) → ●(7) → None

# Step 1: temp = self.head (points to 11)
# Step 2: while temp is not None: (11 ≠ None, so continue)
#         print(temp.value)      # Prints: 11
#         temp = temp.next       # Move to node with 3

# Step 3: while temp is not None: (3 ≠ None, so continue)  
#         print(temp.value)      # Prints: 3
#         temp = temp.next       # Move to node with 23

# Step 4: while temp is not None: (23 ≠ None, so continue)
#         print(temp.value)      # Prints: 23  
#         temp = temp.next       # Move to node with 7

# Step 5: while temp is not None: (7 ≠ None, so continue)
#         print(temp.value)      # Prints: 7
#         temp = temp.next       # Move to None

# Step 6: while temp is not None: (None = None, so stop)
```

**Note:** This is a custom helper method, not a built-in Python method.

---

## 6. Core Methods Implementation

### 6.1 Append Method

**Purpose:** Add a new node to the end of the linked list.

```python
def append(self, value):
    new_node = Node(value)
    
    # Edge case: empty list
    if self.head is None:
        self.head = new_node
        self.tail = new_node
    else:
        # Normal case: list has items
        self.tail.next = new_node  # Link current tail to new node
        self.tail = new_node       # Move tail to new node
    
    self.length += 1
    return True  # Optional: for use in other methods
```

### Append Examples

**Example 1: Adding to empty list**
```python
my_list = LinkedList(1)  # Creates list with just node(1)
my_list.append(2)        # Add node(2) to end

# Result: HEAD → ●(1) → ●(2) → None
#                        ↑
#                      TAIL
```

**Example 2: Adding to existing list**
```python
# Before: HEAD → ●(1) → ●(2) → None
my_list.append(3)
# After:  HEAD → ●(1) → ●(2) → ●(3) → None
```

### 6.2 Pop Method (Remove from End)

**Purpose:** Remove and return the last node from the linked list.

```python
def pop(self):
    # Edge case 1: empty list
    if self.length == 0:
        return None
    
    # Find the second-to-last node
    temp = self.head
    pre = self.head
    
    # Traverse to the end
    while temp.next:
        pre = temp
        temp = temp.next
    
    # Update tail and break connection
    self.tail = pre
    self.tail.next = None
    self.length -= 1
    
    # Edge case 2: was the last node
    if self.length == 0:
        self.head = None
        self.tail = None
    
    return temp
```

### Pop Step-by-Step Example

```python
# Initial: HEAD → ●(1) → ●(2) → ●(3) → None
#                                 ↑
#                               TAIL

# Step 1: temp = head, pre = head (both point to node 1)
# Step 2: while temp.next (node 1's next exists):
#         pre = temp (pre points to node 1)  
#         temp = temp.next (temp points to node 2)
# Step 3: while temp.next (node 2's next exists):
#         pre = temp (pre points to node 2)
#         temp = temp.next (temp points to node 3)  
# Step 4: while temp.next (node 3's next is None, so stop)

# Now: pre points to node 2, temp points to node 3
# Step 5: self.tail = pre (tail points to node 2)
# Step 6: self.tail.next = None (break connection)
# Step 7: return temp (return node 3)

# Result: HEAD → ●(1) → ●(2) → None
#                        ↑
#                      TAIL
```

### 6.3 Prepend Method

**Purpose:** Add a new node to the beginning of the linked list.

```python
def prepend(self, value):
    new_node = Node(value)
    
    # Edge case: empty list
    if self.length == 0:
        self.head = new_node
        self.tail = new_node
    else:
        # Normal case
        new_node.next = self.head  # New node points to current head
        self.head = new_node       # Head points to new node
    
    self.length += 1
    return True
```

### Prepend Example

```python
# Before: HEAD → ●(2) → ●(3) → None
my_list.prepend(1)
# After:  HEAD → ●(1) → ●(2) → ●(3) → None

# Step-by-step:
# 1. Create new_node with value 1
# 2. new_node.next = self.head (new node points to node 2)  
# 3. self.head = new_node (head points to new node)
```

### 6.4 Pop First Method

**Purpose:** Remove and return the first node from the linked list.

```python
def pop_first(self):
    # Edge case: empty list
    if self.length == 0:
        return None
    
    # Store reference to first node
    temp = self.head
    
    # Move head to second node
    self.head = self.head.next
    
    # Break connection
    temp.next = None
    
    # Update length
    self.length -= 1
    
    # Edge case: was the last node
    if self.length == 0:
        self.tail = None
    
    return temp
```

### Pop First Example

```python
# Before: HEAD → ●(1) → ●(2) → ●(3) → None
result = my_list.pop_first()
# After:         HEAD → ●(2) → ●(3) → None
# result points to the removed node ●(1)

print(result.value)  # Output: 1
```

### 6.5 Get Method

**Purpose:** Return the node at a specific index.

```python
def get(self, index):
    # Check for valid index
    if index < 0 or index >= self.length:
        return None
    
    # Traverse to the index
    temp = self.head
    for _ in range(index):
        temp = temp.next
    
    return temp
```

### Get Example

```python
# List: HEAD → ●(0) → ●(1) → ●(2) → ●(3) → None
#       index   0      1      2      3

node = my_list.get(2)
print(node.value)  # Output: 2

# Step-by-step for get(2):
# 1. temp = self.head (points to node with value 0)
# 2. First iteration: temp = temp.next (points to node with value 1)  
# 3. Second iteration: temp = temp.next (points to node with value 2)
# 4. Return temp (node with value 2)
```

### 6.6 Set Value Method

**Purpose:** Change the value of the node at a specific index.

```python
def set_value(self, index, value):
    temp = self.get(index)  # Reuse get method
    
    if temp:  # If get returned a valid node
        temp.value = value
        return True
    return False  # Invalid index
```

### Set Value Example

```python
# Before: HEAD → ●(11) → ●(3) → ●(23) → ●(7) → None
#         index    0       1      2       3

my_list.set_value(1, 4)  # Change value at index 1 to 4

# After:  HEAD → ●(11) → ●(4) → ●(23) → ●(7) → None
#         index    0       1      2       3
```

### 6.7 Insert Method

**Purpose:** Insert a new node at a specific index.

```python
def insert(self, index, value):
    # Check for valid index
    if index < 0 or index > self.length:
        return False
    
    # Special cases
    if index == 0:
        return self.prepend(value)
    if index == self.length:
        return self.append(value)
    
    # General case: insert in middle
    new_node = Node(value)
    temp = self.get(index - 1)  # Get node before insertion point
    
    new_node.next = temp.next   # New node points to next node
    temp.next = new_node        # Previous node points to new node
    
    self.length += 1
    return True
```

### Insert Example

```python
# Before: HEAD → ●(0) → ●(2) → None
#         index   0      1

my_list.insert(1, 1)  # Insert value 1 at index 1

# After:  HEAD → ●(0) → ●(1) → ●(2) → None  
#         index   0      1      2

# Step-by-step:
# 1. temp = get(0) (points to node with value 0)
# 2. new_node.next = temp.next (new node points to node with value 2)
# 3. temp.next = new_node (node 0 points to new node)
```

### 6.8 Remove Method

**Purpose:** Remove and return the node at a specific index.

```python
def remove(self, index):
    # Check for valid index
    if index < 0 or index >= self.length:
        return None
    
    # Special cases
    if index == 0:
        return self.pop_first()
    if index == self.length - 1:
        return self.pop()
    
    # General case: remove from middle
    previous = self.get(index - 1)
    temp = previous.next
    
    previous.next = temp.next  # Bridge the gap
    temp.next = None           # Break connection
    
    self.length -= 1
    return temp
```

### Remove Example

```python
# Before: HEAD → ●(11) → ●(3) → ●(23) → ●(7) → None
#         index    0       1      2       3

removed_node = my_list.remove(2)  # Remove node at index 2

# After:  HEAD → ●(11) → ●(3) → ●(7) → None
#         index    0       1      2

print(removed_node.value)  # Output: 23
```

---

## 7. Advanced Operations

### 7.1 Reverse Method

**Purpose:** Reverse the order of all nodes in the linked list.

**⚠️ Important:** This is a very common interview question!

```python
def reverse(self):
    # Step 1: Swap head and tail
    temp = self.head
    self.head = self.tail
    self.tail = temp
    
    # Step 2: Initialize variables for traversal
    after = temp.next
    before = None
    
    # Step 3: Reverse all the links
    for _ in range(self.length):
        after = temp.next      # Store next node
        temp.next = before     # Reverse the link
        before = temp          # Move before forward
        temp = after           # Move temp forward
```

### Reverse Step-by-Step Example

```python
# Initial: HEAD → ●(1) → ●(2) → ●(3) → ●(4) → None
#                                        ↑
#                                      TAIL

# Step 1: Swap head and tail
# HEAD and TAIL are now swapped (but links aren't reversed yet)

# Step 2: Initialize variables
# temp = original head (node 1)
# after = temp.next (node 2)  
# before = None

# Iteration 1:
# after = temp.next (node 2)
# temp.next = before (node 1 now points to None)
# before = temp (before points to node 1)
# temp = after (temp points to node 2)
# Result: None ← ●(1)    ●(2) → ●(3) → ●(4) → None

# Iteration 2:  
# after = temp.next (node 3)
# temp.next = before (node 2 now points to node 1)
# before = temp (before points to node 2)
# temp = after (temp points to node 3)
# Result: None ← ●(1) ← ●(2)    ●(3) → ●(4) → None

# Iteration 3:
# after = temp.next (node 4)
# temp.next = before (node 3 now points to node 2)  
# before = temp (before points to node 3)
# temp = after (temp points to node 4)
# Result: None ← ●(1) ← ●(2) ← ●(3)    ●(4) → None

# Iteration 4:
# after = temp.next (None)
# temp.next = before (node 4 now points to node 3)
# before = temp (before points to node 4)
# temp = after (temp points to None)
# Final: None ← ●(1) ← ●(2) ← ●(3) ← ●(4)
#        ↑                           ↑
#      TAIL                        HEAD
```

**Critical Points:**
1. The order of operations in the loop is crucial
2. `after` must be updated before changing `temp.next`
3. `before` must be updated before moving `temp`
4. All four steps must be in the exact order shown

---

## 8. Practice Exercises

### Exercise 1: Basic Operations
```python
# Create a linked list and perform basic operations
ll = LinkedList(1)
ll.append(2)
ll.append(3)
ll.prepend(0)

# What does the list look like now?
# Answer: 0 → 1 → 2 → 3 → None

print(ll.get(2).value)  # What will this print?
# Answer: 2
```

### Exercise 2: Edge Cases
```python
# Test edge cases
ll = LinkedList(5)

# What happens with these operations?
result1 = ll.pop()      # Remove only element
result2 = ll.pop()      # Try to pop from empty list
result3 = ll.get(-1)    # Invalid index
result4 = ll.get(0)     # Index on empty list

# Answers:
# result1: Returns node with value 5
# result2: Returns None  
# result3: Returns None
# result4: Returns None
```

### Exercise 3: Complex Operations
```python
# Build: 1 → 2 → 3 → 4 → 5
ll = LinkedList(3)
ll.prepend(2)
ll.prepend(1) 
ll.append(4)
ll.append(5)

# Now perform:
ll.insert(2, 10)    # Insert 10 at index 2
ll.remove(4)        # Remove element at index 4
ll.set_value(1, 20) # Change index 1 to value 20

# What's the final list?
# Answer: 1 → 20 → 10 → 3 → 5
```

### Exercise 4: Reverse Challenge
```python
# Given: A → B → C → D → None
# After reverse: D → C → B → A → None

# Try to trace through the reverse algorithm step by step
# for a 3-node list: X → Y → Z → None
```

### Exercise 5: Implementation Challenge

**Challenge:** Implement a method to find the middle node of a linked list in one pass (without counting length first).

**Hint:** Use two pointers - one moving at normal speed, one moving twice as fast.

```python
def find_middle(self):
    # Your implementation here
    pass
```

**Solution:**
```python
def find_middle(self):
    slow = self.head
    fast = self.head
    
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    
    return slow
```

---

## Summary

### Key Takeaways

1. **Memory Layout**: Linked lists use non-contiguous memory, connected by pointers
2. **Trade-offs**: Better insertion/deletion at beginning, worse random access
3. **Implementation**: Always handle edge cases (empty list, single node)
4. **Traversal**: Must start from head and follow next pointers
5. **Interview Prep**: Master the reverse operation - it's commonly asked

### When to Use Linked Lists

**Good for:**
- Frequent insertion/deletion at the beginning
- Unknown or dynamic size
- Memory is fragmented  
- Don't need random access by index

**Bad for:**
- Frequent random access by index
- Memory usage is a concern (extra pointer storage)
- Cache performance is important
- Frequent access to the last element

### Complete Implementation Summary

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

class LinkedList:
    def __init__(self, value):
        new_node = Node(value)
        self.head = new_node
        self.tail = new_node
        self.length = 1
    
    def print_list(self): # O(n)
    def append(self, value): # O(1)  
    def pop(self): # O(n)
    def prepend(self, value): # O(1)
    def pop_first(self): # O(1)
    def get(self, index): # O(n)
    def set_value(self, index, value): # O(n)
    def insert(self, index, value): # O(n)
    def remove(self, index): # O(n)
    def reverse(self): # O(n)
```

This implementation provides a solid foundation for understanding linked lists and prepares you for technical interviews and real-world applications.
