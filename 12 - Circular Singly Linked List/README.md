# Complete Guide to Circular Singly Linked List in Python

## Table of Contents
1. [Introduction to Circular Singly Linked List](#introduction)
2. [Node Class Implementation](#node-class)
3. [Circular Singly Linked List Class Creation](#class-creation)
4. [Core Methods Implementation](#core-methods)
5. [Time and Space Complexity Analysis](#complexity-analysis)
6. [Complete Implementation](#complete-implementation)

## 1. Introduction to Circular Singly Linked List 

A **Circular Singly Linked List** is exactly the same as a regular singly linked list with one crucial difference:

- **Regular Singly Linked List**: The last node points to `None`
- **Circular Singly Linked List**: The last node points to the first node

### Visual Representation
```
Regular Singly Linked List:
[10] -> [20] -> [30] -> [40] -> None

Circular Singly Linked List:
[10] -> [20] -> [30] -> [40] -> (points back to 10)
```

### Key Characteristics
- The last node's `next` reference points to the first node
- Creates a circular structure with no `None` termination
- Allows infinite traversal if not handled properly
- Head points to the first node, Tail points to the last node

## 2. Node Class Implementation {#node-class}

The Node class remains identical to a regular singly linked list:

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None
    
    def __str__(self):
        return str(self.value)
```

**Key Points:**
- Each node contains a `value` and a `next` pointer
- Initially `next` points to `None`
- The `__str__` method allows easy printing of node values

## 3. Circular Singly Linked List Class Creation 

There are two approaches to create a Circular Singly Linked List:

### Approach 1: Create with One Element
```python
class CSLinkedList:
    def __init__(self, value):
        new_node = Node(value)
        new_node.next = new_node  # Points to itself
        self.head = new_node
        self.tail = new_node
        self.length = 1
```

### Approach 2: Create Empty List (Recommended)
```python
class CSLinkedList:
    def __init__(self):
        self.head = None
        self.tail = None
        self.length = 0
```

**Time Complexity:** O(1)  
**Space Complexity:** O(1)

## 4. Core Methods Implementation {#core-methods}

### 4.1 String Representation (`__str__` method)

```python
def __str__(self):
    temp_node = self.head
    result = ''
    while temp_node is not None:
        result += str(temp_node.value)
        temp_node = temp_node.next
        if temp_node == self.head:  # Stop condition for circular list
            break
        result += ' -> '
    return result
```

**Key Points:**
- Must include break condition to prevent infinite loop
- Checks if `temp_node == self.head` after moving to next
- Builds string representation with arrows between values

**Example Output:**
```python
linked_list = CSLinkedList()
linked_list.append(10)
linked_list.append(20)
print(linked_list)  # Output: "10 -> 20"
```

### 4.2 Append Method (Add at End)

```python
def append(self, value):
    new_node = Node(value)
    if self.length == 0:  # Empty list case
        self.head = new_node
        self.tail = new_node
        new_node.next = new_node  # Points to itself
    else:  # Non-empty list case
        self.tail.next = new_node  # Last node points to new node
        new_node.next = self.head  # New node points to first node
        self.tail = new_node       # Update tail to new node
    self.length += 1
```

**Steps for Non-Empty List:**
1. Create new node
2. Update last node's next to point to new node
3. Update new node's next to point to first node
4. Update tail to point to new node
5. Increment length

**Time Complexity:** O(1)  
**Space Complexity:** O(1)

**Example:**
```python
linked_list = CSLinkedList()
linked_list.append(10)
linked_list.append(20)
linked_list.append(30)
print(linked_list)  # Output: "10 -> 20 -> 30"
```

### 4.3 Prepend Method (Add at Beginning)

```python
def prepend(self, value):
    new_node = Node(value)
    if self.length == 0:  # Empty list case
        self.head = new_node
        self.tail = new_node
        new_node.next = new_node
    else:  # Non-empty list case
        new_node.next = self.head     # New node points to current first
        self.head = new_node          # Update head to new node
        self.tail.next = new_node     # Last node points to new first
    self.length += 1
```

**Steps for Non-Empty List:**
1. Create new node
2. New node's next points to current first node
3. Update head to point to new node
4. Update last node's next to point to new first node
5. Increment length

**Time Complexity:** O(1)  
**Space Complexity:** O(1)

**Example:**
```python
linked_list = CSLinkedList()
linked_list.append(20)
linked_list.append(30)
linked_list.prepend(10)
print(linked_list)  # Output: "10 -> 20 -> 30"
```

### 4.4 Insert Method (Add at Specific Index)

```python
def insert(self, index, value):
    if index < 0 or index > self.length:
        raise Exception("Index out of range")
    
    new_node = Node(value)
    
    if index == 0:  # Insert at beginning
        if self.length == 0:  # Empty list
            self.head = new_node
            self.tail = new_node
            new_node.next = new_node
        else:  # Non-empty list
            new_node.next = self.head
            self.head = new_node
            self.tail.next = new_node
    elif index == self.length:  # Insert at end
        self.tail.next = new_node
        new_node.next = self.head
        self.tail = new_node
    else:  # Insert in middle
        temp_node = self.head
        for _ in range(index - 1):
            temp_node = temp_node.next
        new_node.next = temp_node.next
        temp_node.next = new_node
    
    self.length += 1
```

**Edge Cases Handled:**
- Empty list (index must be 0)
- Insert at beginning (index = 0)
- Insert at end (index = length)
- Insert in middle (0 < index < length)
- Invalid index (< 0 or > length)

**Time Complexity:** O(n) - due to traversal in worst case  
**Space Complexity:** O(1)

**Example:**
```python
linked_list = CSLinkedList()
linked_list.append(10)
linked_list.append(30)
linked_list.insert(1, 20)  # Insert 20 at index 1
print(linked_list)  # Output: "10 -> 20 -> 30"
```

### 4.5 Traversal Method

```python
def traverse(self):
    if not self.head:  # Empty list check
        return
    current = self.head
    while current is not None:
        print(current.value)
        current = current.next
        if current == self.head:  # Stop condition
            break
```

**Key Points:**
- Visits each node exactly once
- Must include break condition to prevent infinite loop
- Handles empty list case

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

### 4.6 Search Method

```python
def search(self, target):
    current = self.head
    index = 0
    while current is not None:
        if current.value == target:
            return index  # Return index where found
        current = current.next
        index += 1
        if current == self.head:  # Prevent infinite loop
            break
    return -1  # Not found
```

**Alternative Version (Boolean Return):**
```python
def search(self, target):
    current = self.head
    while current is not None:
        if current.value == target:
            return True
        current = current.next
        if current == self.head:
            break
    return False
```

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

**Example:**
```python
linked_list = CSLinkedList()
linked_list.append(10)
linked_list.append(20)
linked_list.append(30)
print(linked_list.search(20))  # Output: 1 (index)
print(linked_list.search(40))  # Output: -1 (not found)
```

### 4.7 Get Method (Access by Index)

```python
def get(self, index):
    if index == -1:  # Special case for last element
        return self.tail
    elif index < -1 or index >= self.length:
        return None
    
    current = self.head
    for _ in range(index):
        current = current.next
    return current
```

**Features:**
- Returns node at specified index
- Supports negative index (-1) for last element
- Returns `None` for invalid indices
- Includes range validation

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

**Example:**
```python
linked_list = CSLinkedList()
linked_list.append(10)
linked_list.append(20)
linked_list.append(30)
node = linked_list.get(1)
print(node.value)  # Output: 20
```

### 4.8 Set Method (Update Value by Index)

```python
def set_value(self, index, value):
    temp = self.get(index)
    if temp:
        temp.value = value
        return True
    return False
```

**Features:**
- Uses `get()` method for node retrieval
- Updates node value if valid index
- Returns `True` for successful update, `False` otherwise

**Time Complexity:** O(n) - due to `get()` method  
**Space Complexity:** O(1)

**Example:**
```python
linked_list = CSLinkedList()
linked_list.append(10)
linked_list.append(20)
success = linked_list.set_value(1, 25)
print(success)  # Output: True
print(linked_list)  # Output: "10 -> 25"
```

### 4.9 Pop First Method (Remove First Element)

```python
def pop_first(self):
    if self.length == 0:
        return None
    
    popped_node = self.head
    
    if self.length == 1:  # Single element case
        self.head = None
        self.tail = None
    else:  # Multiple elements case
        self.head = self.head.next      # Move head to second node
        self.tail.next = self.head      # Last node points to new head
        popped_node.next = None         # Disconnect popped node
    
    self.length -= 1
    return popped_node
```

**Edge Cases:**
- Empty list: Return `None`
- Single element: Set head and tail to `None`
- Multiple elements: Update pointers appropriately

**Time Complexity:** O(1)  
**Space Complexity:** O(1)

**Example:**
```python
linked_list = CSLinkedList()
linked_list.append(10)
linked_list.append(20)
linked_list.append(30)
popped = linked_list.pop_first()
print(popped.value)  # Output: 10
print(linked_list)   # Output: "20 -> 30"
```

### 4.10 Pop Method (Remove Last Element)

```python
def pop(self):
    if self.length == 0:
        return None
    
    popped_node = self.tail
    
    if self.length == 1:  # Single element case
        self.head = None
        self.tail = None
    else:  # Multiple elements case
        temp = self.head
        while temp.next != self.tail:  # Find second-to-last node
            temp = temp.next
        temp.next = self.head          # Second-to-last points to head
        self.tail = temp               # Update tail to second-to-last
    
    popped_node.next = None
    self.length -= 1
    return popped_node
```

**Steps for Multiple Elements:**
1. Find second-to-last node by traversal
2. Update second-to-last node's next to point to head
3. Update tail to point to second-to-last node
4. Disconnect popped node
5. Decrement length

**Time Complexity:** O(n) - due to traversal to find second-to-last  
**Space Complexity:** O(1)

**Example:**
```python
linked_list = CSLinkedList()
linked_list.append(10)
linked_list.append(20)
linked_list.append(30)
popped = linked_list.pop()
print(popped.value)  # Output: 30
print(linked_list)   # Output: "10 -> 20"
```

### 4.11 Remove Method (Remove by Index)

```python
def remove(self, index):
    if index < -1 or index >= self.length:
        return None
    if index == 0:
        return self.pop_first()
    if index == -1 or index == self.length - 1:
        return self.pop()
    
    prev_node = self.get(index - 1)
    popped_node = prev_node.next
    prev_node.next = popped_node.next
    popped_node.next = None
    self.length -= 1
    return popped_node
```

**Edge Cases Handled:**
- Invalid index: Return `None`
- Remove first (index 0): Use `pop_first()`
- Remove last (index -1 or length-1): Use `pop()`
- Remove middle: Standard removal logic

**Time Complexity:** O(n) - due to `get()` method for finding previous node  
**Space Complexity:** O(1)

**Example:**
```python
linked_list = CSLinkedList()
linked_list.append(10)
linked_list.append(20)
linked_list.append(30)
removed = linked_list.remove(1)
print(removed.value)  # Output: 20
print(linked_list)    # Output: "10 -> 30"
```

### 4.12 Delete All Method (Clear List)

```python
def delete_all(self):
    if self.length == 0:
        return  # Already empty
    
    self.tail.next = None  # Break circular link
    self.head = None
    self.tail = None
    self.length = 0
```

**Steps:**
1. Check if list is already empty
2. Break circular connection (tail.next = None)
3. Set head and tail to None
4. Reset length to 0
5. Garbage collector removes unreferenced nodes

**Time Complexity:** O(1)  
**Space Complexity:** O(1)

**Example:**
```python
linked_list = CSLinkedList()
linked_list.append(10)
linked_list.append(20)
linked_list.delete_all()
print(linked_list)  # Output: "" (empty)
```

## 5. Time and Space Complexity Analysis {#complexity-analysis}

| Operation | Time Complexity | Space Complexity | Notes |
|-----------|----------------|------------------|-------|
| Creation | O(1) | O(1) | Empty list initialization |
| Append | O(1) | O(1) | Add at end |
| Prepend | O(1) | O(1) | Add at beginning |
| Insert | O(n) | O(1) | Worst case: traverse to index |
| Search | O(n) | O(1) | Linear search through all nodes |
| Traverse | O(n) | O(1) | Visit all nodes once |
| Get | O(n) | O(1) | Access by index requires traversal |
| Set | O(n) | O(1) | Uses get() method |
| Pop First | O(1) | O(1) | Direct access to head |
| Pop | O(n) | O(1) | Must find second-to-last node |
| Remove | O(n) | O(1) | Uses get() for finding previous |
| Delete All | O(1) | O(1) | Simple pointer updates |

## 6. Complete Implementation {#complete-implementation}

Here's a complete working example with all methods:

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None
    
    def __str__(self):
        return str(self.value)

class CSLinkedList:
    def __init__(self):
        self.head = None
        self.tail = None
        self.length = 0
    
    def __str__(self):
        temp_node = self.head
        result = ''
        while temp_node is not None:
            result += str(temp_node.value)
            temp_node = temp_node.next
            if temp_node == self.head:
                break
            result += ' -> '
        return result
    
    def append(self, value):
        new_node = Node(value)
        if self.length == 0:
            self.head = new_node
            self.tail = new_node
            new_node.next = new_node
        else:
            self.tail.next = new_node
            new_node.next = self.head
            self.tail = new_node
        self.length += 1
    
    def prepend(self, value):
        new_node = Node(value)
        if self.length == 0:
            self.head = new_node
            self.tail = new_node
            new_node.next = new_node
        else:
            new_node.next = self.head
            self.head = new_node
            self.tail.next = new_node
        self.length += 1
    
    # ... (include all other methods as shown above)

# Example Usage
if __name__ == "__main__":
    linked_list = CSLinkedList()
    
    # Test append
    linked_list.append(10)
    linked_list.append(20)
    linked_list.append(30)
    print("After append:", linked_list)
    
    # Test prepend
    linked_list.prepend(5)
    print("After prepend:", linked_list)
    
    # Test insert
    linked_list.insert(2, 15)
    print("After insert:", linked_list)
    
    # Test search
    print("Search 15:", linked_list.search(15))
    
    # Test get and set
    node = linked_list.get(1)
    print("Get index 1:", node.value if node else None)
    linked_list.set_value(1, 25)
    print("After set:", linked_list)
    
    # Test remove operations
    popped_first = linked_list.pop_first()
    print("Popped first:", popped_first.value if popped_first else None)
    print("After pop_first:", linked_list)
    
    popped_last = linked_list.pop()
    print("Popped last:", popped_last.value if popped_last else None)
    print("After pop:", linked_list)
    
    # Test traversal
    print("Traversal:")
    linked_list.traverse()
```

### Key Implementation Tips

1. **Always include break conditions** in loops to prevent infinite traversal
2. **Handle edge cases** for empty lists and single-element lists
3. **Maintain circular property** by ensuring last node always points to first
4. **Update length** in all modification operations
5. **Validate indices** in methods that accept index parameters
6. **Use existing methods** where possible (e.g., `remove()` uses `pop_first()` and `pop()`)

This comprehensive implementation provides a fully functional Circular Singly Linked List with all standard operations and proper error handling.
