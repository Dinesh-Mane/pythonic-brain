# Linked List
A Linked List is a linear data structure where each element (called a Node) contains:
- Data (value)
- Pointer (reference) to the next node

# Structure of a Node
Each node can be represented using a class in Python:
```python
class Node:
    def __init__(self, val):
        self.val = val
        self.next = None
```
- `val`: holds the value
- `next`: points to the next node (or None if it's the last)


## Advantages : 
|  Advantage                               |  Explanation                                                                                              |
| ----------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| **Dynamic size**                          | No need to define size in advance like arrays — can grow/shrink on the fly.                                 |
| **Efficient Insert/Delete (O(1))**        | Insertions and deletions at the head or tail can be done in constant time (no shifting needed like arrays). |
| **No memory waste**                       | Only allocates memory for used elements, unlike arrays which may over-allocate.                             |
| **Implementation of abstract data types** | Used to build Stacks, Queues, Hash Maps (chaining), Graphs (adjacency list), etc.                           |
| **Easy node manipulation**                | Reordering elements is easier — especially useful in linked list-based sorting or reversal problems.        |
| **Faster deletion in middle**             | Once you have the previous node, deletion is O(1). No shifting like arrays.                                 |

## Disadvantages :
|  Disadvantage                |  Explanation                                                                                               |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------ |
| **Slow access time (O(n))**   | No random access. You must traverse from the head to reach the `n`th node.                                   |
| **Extra memory overhead**     | Each node needs additional memory for the pointer (`.next`, or `.prev` in doubly LL).                        |
| **Cache inefficiency**        | Not cache-friendly due to non-contiguous memory allocation — poor CPU cache utilization.                     |
| **Reverse traversal is hard** | In a singly linked list, you can't go backward unless you use a doubly linked list.                          |
| **Complex to implement**      | Especially compared to simple Python lists — more logic needed for pointer manipulation.                     |
| **Hard to debug**             | Mistakes in pointer updates (like missing `.next`) can silently break the structure or cause infinite loops. |

## When to Prefer Linked List over Array?
| Situation                                       | Use Linked List?               |
| ----------------------------------------------- | ------------------------------ |
| Unknown size in advance                         | ✅ Yes                          |
| Frequent insert/delete at head/middle           | ✅ Yes                          |
| Need fast access to random elements             | ❌ No (use array)               |
| Memory is constrained                           | ❌ No (pointer overhead)        |
| You need constant resizing without reallocating | ✅ Yes                          |
| You need to sort/search often                   | ❌ No (arrays/lists are better) |

## Interview Insight : 
| Interviewer May Ask           | What to Say                                                                               |
| ----------------------------- | ----------------------------------------------------------------------------------------- |
| “Why use a linked list here?” | "Because I need dynamic size and fast insertions/deletions."                              |
| “Why not array?”              | "Because arrays are fixed-size and inserting in middle is costly (O(n)) due to shifting." |

## Types of Linked Lists
| Type                     | Description                                 |
| ------------------------ | ------------------------------------------- |
| **Singly Linked List**   | Each node points to next node only          |
| **Doubly Linked List**   | Each node points to next and previous nodes |
| **Circular Linked List** | Last node points to the head                |
| **Circular Doubly**      | Combo of doubly + circular                  |

# Linked List Operations
First, Define the Node and LinkedList Classes
```python
class Node:
    def __init__(self, val):
        self.val = val
        self.next = None
        
class LinkedList:
    def __init__(self):
        self.head = None
```

## 1. Insert at Head (O(1))
**Problem type:** insert a new node at the beginning (i.e., head/front) of the linked list.
```python
def insert_at_head(self, val):
    new_node = Node(val)
    new_node.next = self.head
    self.head = new_node
```
> New node gets inserted at the beginning, and becomes the new head of the list.

Dry Run:  
| Operation            | Linked List State     |
| -------------------- | --------------------- |
| Initially empty      | `None`                |
| insert\_at\_head(10) | `10 → None`           |
| insert\_at\_head(20) | `20 → 10 → None`      |
| insert\_at\_head(30) | `30 → 20 → 10 → None` |

## 2. Insert at Tail (O(n))
**Problem type:** Insert a new node at the end (tail) of the linked list.
```python
def insert_at_tail(self, val):
    new_node = Node(val)
    if not self.head:
        self.head = new_node
        return
    curr = self.head
    while curr.next:
        curr = curr.next
    curr.next = new_node
```
> Traverse the list until you reach the last node, then attach the new node at the end. If the list is empty, the new node becomes the head.

Dry Run:  
| Operation            | Linked List State     |
| -------------------- | --------------------- |
| Initially empty      | `None`                |
| insert\_at\_tail(10) | `10 → None`           |
| insert\_at\_tail(20) | `10 → 20 → None`      |
| insert\_at\_tail(30) | `10 → 20 → 30 → None` |


## 3. Insert at Specific Position (O(n))
**Problem type:** Insert a new node at a given 0-based index position in the linked list.
```python
def insert_at_position(self, val, pos):
    if pos == 0:
        self.insert_at_head(val)
        return
    new_node = Node(val)
    curr = self.head
    for _ in range(pos - 1):
        if not curr:
            return  # Invalid position
        curr = curr.next
    new_node.next = curr.next
    curr.next = new_node
```
> Traverse to the node at `pos - 1`, then adjust pointers to insert the new node at the desired position. If `pos == 0`, insert at head.

Dry Run:  
| Operation                   | Linked List State          |
| --------------------------- | -------------------------- |
| Initially empty             | `None`                     |
| insert\_at\_position(10, 0) | `10 → None`                |
| insert\_at\_position(20, 1) | `10 → 20 → None`           |
| insert\_at\_position(30, 1) | `10 → 30 → 20 → None`      |
| insert\_at\_position(40, 2) | `10 → 30 → 40 → 20 → None` |


## 4. Delete Node by Value (O(n))
**Problem type:** Delete the first node in the linked list that contains the given value.
```python
def delete_by_value(self, value):
    if not self.head:
        return  # Empty list
    if self.head.val == value:
        self.head = self.head.next  # Delete head
        return
    prev = None
    curr = self.head
    while curr and curr.val != value:
        prev = curr
        curr = curr.next
    if curr:
        prev.next = curr.next  # Bypass the node with matching value
```
> Traverse the list and remove the first node with the given value by changing pointers. If the value is in the head, move the head pointer.

Dry Run:  
| Operation              | Linked List State               |
| ---------------------- | ------------------------------- |
| Initially empty        | `None`                          |
| insert\_at\_tail(10)   | `10 → None`                     |
| insert\_at\_tail(20)   | `10 → 20 → None`                |
| insert\_at\_tail(30)   | `10 → 20 → 30 → None`           |
| delete\_by\_value(20)  | `10 → 30 → None`                |
| delete\_by\_value(10)  | `30 → None`                     |
| delete\_by\_value(100) | `30 → None` *(value not found)* |


## 5. Delete at Position (O(n))
**Problem type:** Delete a node at a given 0-based index position from the linked list.
```python
def delete_at_position(self, pos):
    if pos == 0:
        self.head = self.head.next
        return
    curr = self.head
    for _ in range(pos - 1):
        if not curr or not curr.next:
            return  # Invalid position
        curr = curr.next
    curr.next = curr.next.next
```
> Traverse to the node just before the given position (pos - 1), and then skip the node at pos by changing pointers. If position is 0, simply move the head to the next node.

Dry Run:  
| Operation               | Linked List State       |
| ----------------------- | ----------------------- |
| Initially empty         | `None`                  |
| insert\_at\_tail(10)    | `10 → None`             |
| insert\_at\_tail(20)    | `10 → 20 → None`        |
| insert\_at\_tail(30)    | `10 → 20 → 30 → None`   |
| delete\_at\_position(1) | `10 → 30 → None`        |
| delete\_at\_position(0) | `30 → None`             |
| delete\_at\_position(5) | `30 → None` *(ignored)* |


## 6. Search a Value (O(n))
**Problem type:** Check whether a given value exists in the linked list or not.
```python
def search(self, target):
    curr = self.head
    while curr:
        if curr.val == target:
            return True
        curr = curr.next
    return False
```
> Start from the head and traverse node-by-node. If you find a node where `data == target`, return `True`. If you reach the end without finding it, return `False`.

Dry Run:  
| Operation            | Linked List State     | Result               |
| -------------------- | --------------------- | -------------------- |
| Initially empty      | `None`                | `search(10) → False` |
| insert\_at\_tail(10) | `10 → None`           | `search(10) → True`  |
| insert\_at\_tail(20) | `10 → 20 → None`      | `search(20) → True`  |
| insert\_at\_tail(30) | `10 → 20 → 30 → None` | `search(25) → False` |
| search(30)           | `10 → 20 → 30 → None` | `True`               |


## 7. Traverse and Print the List (O(n))
**Problem type:** Print all the nodes in the linked list from head to tail.
```python
def print_list(self):
    curr = self.head
    while curr:
        print(curr.val, end=" → ")
        curr = curr.next
    print("None")
```
> Traverse through each node starting from the head and print its value, followed by an arrow (`→`). When the end of the list is reached, print `None` to indicate the end.

Dry Run:  
| Operation            | Linked List State     | Output                |
| -------------------- | --------------------- | --------------------- |
| Initially empty      | `None`                | `None`                |
| insert\_at\_tail(10) | `10 → None`           | `10 → None`           |
| insert\_at\_tail(20) | `10 → 20 → None`      | `10 → 20 → None`      |
| insert\_at\_tail(30) | `10 → 20 → 30 → None` | `10 → 20 → 30 → None` |

## 8. Count Length (Iterative) (O(n))
**Problem type:** Count the total number of nodes in the linked list.
```python
def length(self):
    count = 0
    curr = self.head
    while curr:
        count += 1
        curr = curr.next
    return count
```
> Traverse the entire linked list and increment the counter for each node. Once you reach the end (`None`), the `count` will hold the total number of nodes.

Dry Run:  
| Operation            | Linked List State     | Result         |
| -------------------- | --------------------- | -------------- |
| Initially empty      | `None`                | `length() → 0` |
| insert\_at\_tail(10) | `10 → None`           | `length() → 1` |
| insert\_at\_tail(20) | `10 → 20 → None`      | `length() → 2` |
| insert\_at\_tail(30) | `10 → 20 → 30 → None` | `length() → 3` |
| length()             | `10 → 20 → 30 → None` | `3`            |


## 9A. Reverse Linked List (Iterative) (O(n))
**Problem type:** Reverse the entire linked list.
```python
def reverse(self):
    prev = None
    curr = self.head
    while curr:
        next_node = curr.next  # Save the next node
        curr.next = prev       # Reverse the current node's pointer
        prev = curr            # Move prev to the current node
        curr = next_node       # Move to the next node
    self.head = prev           # Set the new head to the last node
```
> Traverse the list and reverse the direction of the next pointers one by one. After all nodes are reversed, the prev pointer will point to the new head.

Dry Run:  
| Operation            | Linked List State     | Result                |
| -------------------- | --------------------- | --------------------- |
| Initially empty      | `None`                | `None`                |
| insert\_at\_tail(10) | `10 → None`           | `10 → None`           |
| insert\_at\_tail(20) | `10 → 20 → None`      | `10 → 20 → None`      |
| insert\_at\_tail(30) | `10 → 20 → 30 → None` | `10 → 20 → 30 → None` |
| reverse()            | `30 → 20 → 10 → None` | `30 → 20 → 10 → None` |

## 9B. Recursive Reversal of Linked List (O(n))
**Problem type:** Reverse the linked list using recursion (from tail back to head).
```python
def reverse_recursive(self, node):
    if node is None or node.next is None:
        return node
    new_head = self.reverse_recursive(node.next)
    node.next.next = node
    node.next = None
    return new_head
```
> Go to the end of the list using recursion (node.next), then reverse pointers while returning from recursion stack.  
> At the end, update self.head = new_head to point to the new head.  

Dry Run:  
| Operation                | Linked List State            | Result (After Reversal) |
| ------------------------ | ---------------------------- | ----------------------- |
| Initially empty          | `None`                       | `None`                  |
| insert\_at\_tail(10)     | `10 → None`                  | `10 → None`             |
| insert\_at\_tail(20)     | `10 → 20 → None`             | `20 → 10 → None`        |
| insert\_at\_tail(30)     | `10 → 20 → 30 → None`        | `30 → 20 → 10 → None`   |
| reverse\_recursive(head) | Recursive Reversal Triggered | Head becomes `30`       |

**After calling reverse_recursive, don’t forget:**
```python
self.head = self.reverse_recursive(self.head)
```

## 10. Find Middle Element (O(n))
**Problem type:** Return the middle node's value in the linked list.
```python
def find_middle(self):
    slow = fast = self.head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    return slow.val if slow else None
```
> Use the Tortoise and Hare Algorithm:  
> `slow` moves one step at a time, `fast` moves two steps.  
> When `fast` reaches the end, `slow` will be at the middle.  

Dry Run:  
| Operation            | Linked List State               | Result                 |
| -------------------- | ------------------------------- | ---------------------- |
| Initially empty      | `None`                          | `find_middle() → None` |
| insert\_at\_tail(10) | `10 → None`                     | `find_middle() → 10`   |
| insert\_at\_tail(20) | `10 → 20 → None`                | `find_middle() → 20`   |
| insert\_at\_tail(30) | `10 → 20 → 30 → None`           | `find_middle() → 20`   |
| insert\_at\_tail(40) | `10 → 20 → 30 → 40 → None`      | `find_middle() → 30`   |
| insert\_at\_tail(50) | `10 → 20 → 30 → 40 → 50 → None` | `find_middle() → 30`   |


## 11. Detect Cycle (Floyd’s Algorithm) (O(n))
**Problem type:** Detect whether the linked list has a cycle (loop) or not.
```python
def has_cycle(self):
    slow = fast = self.head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False
```
> Use two pointers (`slow` and `fast`). `slow` moves one step, `fast` moves two steps.  
> If there's a cycle, they will eventually meet. If there's no cycle, `fast` will hit the end (`None`).

Dry Run:  
| Operation             | Linked List State        | Result                |
| --------------------- | ------------------------ | --------------------- |
| Initially empty       | `None`                   | `has_cycle() → False` |
| insert\_at\_tail(10)  | `10 → None`              | `has_cycle() → False` |
| insert\_at\_tail(20)  | `10 → 20 → None`         | `has_cycle() → False` |
| insert\_at\_tail(30)  | `10 → 20 → 30 → None`    | `has_cycle() → False` |
| manually create cycle | `30.next = 20` (20 ← 30) | `has_cycle() → True`  |


## 12. Merge Two Sorted Linked Lists (O(n + m))
**Problem type:** Merge two sorted singly linked lists into one sorted list.
```python
def merge_sorted_lists(l1, l2):
    dummy = Node(-1)
    curr = dummy
    while l1 and l2:
        if l1.data < l2.data:
            curr.next = l1
            l1 = l1.next
        else:
            curr.next = l2
            l2 = l2.next
        curr = curr.next
    curr.next = l1 if l1 else l2
    return dummy.next
```
> Start with a dummy node and compare elements from both lists.  
> Attach the smaller node and move forward.  
> Once one list is finished, attach the remaining part of the other list.  

Dry Run:  
| Operation               | l1 State           | l2 State           | Merged Result           |
| ----------------------- | ------------------ | ------------------ | ----------------------- |
| Initially both empty    | `None`             | `None`             | `None`                  |
| l1 = 1 → 3 → 5          | `1 → 3 → 5 → None` | `None`             | `1 → 3 → 5 → None`      |
| l2 = 2 → 4 → 6          | `1 → 3 → 5 → None` | `2 → 4 → 6 → None` | `1 → 2 → 3 → 4 → 5 → 6` |
| l1 = 1 → 4 → 7          | `1 → 4 → 7 → None` | `2 → 3 → 5 → None` | `1 → 2 → 3 → 4 → 5 → 7` |
| l1 = None, l2 not empty | `None`             | `10 → 20 → None`   | `10 → 20 → None`        |


## 13. Full Example with All Ops:
```python
ll = LinkedList()
ll.insert_at_head(3)
ll.insert_at_head(2)
ll.insert_at_head(1)
ll.insert_at_tail(4)
ll.print_list()          # 1 → 2 → 3 → 4 → None

ll.reverse()
ll.print_list()          # 4 → 3 → 2 → 1 → None

print(ll.search(3))      # True
print(ll.length())       # 4

ll.delete_by_value(3)
ll.print_list()          # 4 → 2 → 1 → None
```










