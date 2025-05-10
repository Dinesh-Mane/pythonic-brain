# List of Data Structures in Python
## 1. Built-in Data Structures
| Data Structure          | Description                                               |
| ----------------------- | --------------------------------------------------------- |
| **`list`**              | Ordered, mutable, allows duplicates. Dynamic arrays.      |
| **`tuple`**             | Ordered, immutable, allows duplicates. Like fixed lists.  |
| **`set`**               | Unordered, mutable, no duplicates. Fast membership tests. |
| **`frozenset`**         | Immutable version of a set. Hashable.                     |
| **`dict` (dictionary)** | Key-value mapping. Ordered (from Python 3.7+), mutable.   |

## 2. From `collections` Module
> Import with: `from collections import ...`

| Data Structure    | Description                                                    |
| ----------------- | -------------------------------------------------------------- |
| **`deque`**       | Double-ended queue. Fast appends/pops from both ends.          |
| **`defaultdict`** | Dictionary with default values for missing keys.               |
| **`OrderedDict`** | Dictionary that remembers insertion order (before Python 3.7). |
| **`Counter`**     | Dictionary subclass for counting hashable objects.             |
| **`ChainMap`**    | Combines multiple dicts and treats them as one.                |
| **`namedtuple`**  | Tuple with named fields (acts like lightweight class).         |

## 3. From `array` Module
> Import with: `from array import array`

| Data Structure | Description                                               |
| -------------- | --------------------------------------------------------- |
| **`array`**    | Fixed-type arrays (more efficient than list for numbers). |

## 4. From `heapq` Module
> Import with: `from collections import ...`

| Data Structure    | Description                                                    |
| ----------------- | -------------------------------------------------------------- |
| **`deque`**       | Double-ended queue. Fast appends/pops from both ends.          |
| **`defaultdict`** | Dictionary with default values for missing keys.               |
| **`OrderedDict`** | Dictionary that remembers insertion order (before Python 3.7). |
| **`Counter`**     | Dictionary subclass for counting hashable objects.             |
| **`ChainMap`**    | Combines multiple dicts and treats them as one.                |
| **`namedtuple`**  | Tuple with named fields (acts like lightweight class).         |

## 5. From `queue` Module
> Import with: `import queue`

| Data Structure      | Description                                        |
| ------------------- | -------------------------------------------------- |
| **`Queue`**         | FIFO queue (first-in, first-out). Thread-safe.     |
| **`LifoQueue`**     | Stack (last-in, first-out). Thread-safe.           |
| **`PriorityQueue`** | Thread-safe priority queue (uses heap internally). |

## 6. Custom/Advanced Data Structures
> We can create these manually or use libraries:

| Structure                     | Description                                               |
| ----------------------------- | --------------------------------------------------------- |
| **Stack**                     | Often implemented using list or `deque`.                  |
| **Queue**                     | Can use list (`pop(0)`), `deque`, or `queue.Queue`.       |
| **Priority Queue**            | Use `heapq` or `queue.PriorityQueue`.                     |
| **Graph**                     | Dictionary of lists or dict of sets, or adjacency matrix. |
| **Tree**                      | Custom classes (BinaryTree, Trie, etc.).                  |
| **LinkedList**                | Custom class (not built-in).                              |
| **HashMap / HashSet**         | Built-in `dict` and `set` act like these.                 |
| **Trie (Prefix Tree)**        | Custom class, useful for string problems.                 |
| **Disjoint Set / Union-Find** | Custom implementation, useful in graph problems.          |


# Brief Explanation: 
Here’s a brief explanation of each Python data structure, categorized for clarity and usefulness in coding interviews, competitive programming, and real-world usage:

## 1. Built-in Data Structures
### 1. `list`
- Ordered, mutable, allows duplicates  ( mutable म्हणजे: changeable )
- Use when: You need a dynamic array (e.g., `[1, 2, 3]`)  
- Operations: `append()`, `pop()`, `sort()`, slicing

```python
fruits = ['apple', 'banana', 'apple']
fruits.append('mango')  # Adds at the end
```
 
### 2. `tuple`
- Ordered, immutable, allows duplicates  
- Use when: Data shouldn't change (e.g., coordinates, `(x, y)`)  
- Faster and more memory-efficient than lists  
```python
point = (3, 4)
# point[0] = 5  # ❌ Error: can't modify tuple
```
### 3. `set`
- Unordered, mutable, no duplicates
- Use when: You need to store unique items quickly
- Fast membership test: x in my_set
- Operations: `add()`, `remove()`, set algebra (`union`, `intersection`)
```python
s = {1, 2, 3}
s.add(2)  # Duplicate ignored
print(2 in s)  # True
```
### 4. `frozenset`
- Immutable version of set
- Can be used as a key in a dictionary
- No `add()` or `remove()`.
```python
fs = frozenset([1, 2, 3])
# fs.add(4)  # ❌ Error: cannot modify
```
### 5. `dict` (Dictionary)
- Key-value store, ordered as of Python 3.7+
- Use when: Mapping one thing to another (e.g., `{'name': 'John'}`)
- Keys must be unique and hashable  (Hashable म्हणजे: "ज्याला बदलता येणार नाही (immutable आहे) आणि ज्याचं एक unique number (hash) बनवता येतं, तो hashable असतो." don't worry... we will learn this in upcomming tutorials.) 
- Operations: `get()`, `items()`, `keys()`, `values()` 
```python
person = {'name': 'Alice', 'age': 30}
person['age'] = 31  # Update value
```
### Summary : 
| Structure   | Ordered | Mutable | Allows Duplicates | Notes                        |
| ----------- | ------- | ------- | ----------------- | ---------------------------- |
| `list`      | ✅       | ✅       | ✅                 | Dynamic array                |
| `tuple`     | ✅       | ❌       | ✅                 | Fixed-size, used as keys     |
| `set`       | ❌       | ✅       | ❌                 | Unique elements only         |
| `frozenset` | ❌       | ❌       | ❌                 | Immutable version of `set`   |
| `dict`      | ✅       | ✅       | ❌ (in keys)       | Key-value store, fast lookup |


## 2. From `collections` Module
### 1. `deque` (Double-ended queue)
- Full form: Double-ended queue
- Use case: When you want to add/remove items from both ends efficiently (left & right).
- Faster than list for `pop(0)` or `insert(0, x)` operations.
```python
from collections import deque

dq = deque()
dq.append(10)      # Add to right
dq.appendleft(5)   # Add to left
dq.pop()           # Remove from right
dq.popleft()       # Remove from left
```

### 2. `defaultdict`
- It's like a normal dictionary, but if key is missing, it gives a default value instead of error.
- Saves you from writing `if key in dict:` checks.
```python
from collections import defaultdict

d = defaultdict(int)  # Default value is 0
d['a'] += 1           # No KeyError!
print(d['a'])         # Output: 1
```

### 3. `OrderedDict`
- It's like a normal dictionary but it remembers the order in which items were added.
- Before Python 3.7, normal `dict` didn't preserve insertion order. `OrderedDict` was used instead.
```python
from collections import OrderedDict

od = OrderedDict()
od['a'] = 1
od['b'] = 2
print(od)  # Output: OrderedDict([('a', 1), ('b', 2)])
```
### 4. `Counter`
- Special dict that counts the frequency of each element.
- Works with any iterable: string, list, etc.
- Useful in frequency-based problems, like finding most common elements.
```python
from collections import Counter

c = Counter("aabccc")
print(c)  # Output: Counter({'c': 3, 'a': 2, 'b': 1})
```

### 5. `ChainMap`
- Combines multiple dictionaries into one view (chain of maps).
- Good for nested scopes or fallback configs (like default + user config).
- It searches keys from left to right in the chain.
```python
from collections import ChainMap

a = {'x': 1, 'y': 2}
b = {'y': 10, 'z': 3}
cm = ChainMap(a, b)
print(cm['y'])  # Output: 2 (from first dict)
```

### 6. `namedtuple`
- Like a normal tuple, but with named fields (like an object/class).
- Lightweight and memory-efficient alternative to class.
- Good for clean code and readable data structures.
```python
from collections import namedtuple

Point = namedtuple('Point', ['x', 'y'])
p = Point(3, 4)
print(p.x, p.y)  # Output: 3 4
```
## 3. From array Module

### 6. `array` (from `array` module)
- It's like a list, but it stores only one data type (e.g., all integers).
- More memory-efficient and faster than lists for large numeric data.

```python
from array import array

arr = array('i', [1, 2, 3, 4])  # 'i' = integer type
arr.append(5)
print(arr)  # Output: array('i', [1, 2, 3, 4, 5])
```

## 4. From `heapq` Module

### 1. `heap (via list)` – Min-Heap using `heapq` module
-  A heap is a special kind of binary tree used for priority queues.
- In Python, heaps are implemented using lists + the `heapq` module.
- By default, it creates a min-heap – smallest element comes out first.

Example (Min-Heap):
```python
import heapq

nums = [5, 2, 8, 1]
heapq.heapify(nums)         # Convert list into heap: [1, 2, 8, 5]
heapq.heappush(nums, 0)     # Add 0 → heap becomes: [0, 1, 8, 5, 2]
smallest = heapq.heappop(nums)  # Removes and returns 0
```
For Max-Heap:  
Python does not have built-in max-heap, but you can negate values:
```python
max_heap = []
heapq.heappush(max_heap, -10)
heapq.heappush(max_heap, -5)
heapq.heappush(max_heap, -20)

max_val = -heapq.heappop(max_heap)  # Output: 20 (max)
```

## 5. From `queue` Module

### 1. `Queue` (FIFO Queue)
- First-In-First-Out (FIFO): Items come out in the same order they went in.
- Thread-safe → good for multi-threaded producer-consumer problems.
- Automatically handles locking.
```python
from queue import Queue

q = Queue()
q.put(10)
q.put(20)
print(q.get())  # Output: 10
```

### 2. `LifoQueue` (Stack)
- Last-In-First-Out (LIFO): Works like a stack.
- Thread-safe version of a stack.
```python
from queue import LifoQueue

stack = LifoQueue()
stack.put(1)
stack.put(2)
print(stack.get())  # Output: 2
```

### 3. `PriorityQueue`
- Items come out based on priority (lowest first by default).
- Internally uses a min-heap.
- Thread-safe → used in concurrent tasks with priorities
```python
from queue import PriorityQueue

pq = PriorityQueue()
pq.put((1, 'low'))    # (priority, value)
pq.put((0, 'urgent'))
print(pq.get())       # Output: (0, 'urgent')
```

## 6. Custom/Advanced Data Structures

### 1. Stack
- LIFO (Last In, First Out) structure.
- Used for undo, expression evaluation, DFS, etc.
- Can use Python `list` (`append()` + `pop()`) or `collections.deque`.

```python
stack = []
stack.append(10)
stack.append(20)
stack.pop()  # 20
```

### 2. Queue
- FIFO (First In, First Out) structure..
- Used in BFS, scheduling, task queues.
- Use `collections.deque` for efficiency (better than list).

```python
from collections import deque
queue = deque()
queue.append(1)
queue.append(2)
queue.popleft()  # 1
```

### 3. Priority Queue
- Elements come out by priority, not insertion order.
- Use heapq for min-heap (default).
- Use queue.PriorityQueue for thread-safe usage.

```python
import heapq
pq = []
heapq.heappush(pq, 3)
heapq.heappush(pq, 1)
heapq.heappop(pq)  # 1 (smallest)
```

### 4. Graph
- Represents relationships/connections (nodes and edges).
- Common formats:
  - `adjacency list`: `{node: [neighbors]}`
  - `adjacency matrix`: 2D list
- Used in pathfinding, networking, dependency resolution.

```python
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D'],
    'C': ['A'],
    'D': ['B']
}
```

### 5. Tree
- Hierarchical structure, one root, many levels.
- Used in parsing, file systems, decision-making (e.g., BST, Trie).
- You must define your own custom classes.

```python
class Node:
    def __init__(self, val):
        self.val = val
        self.left = self.right = None
```

### 6. LinkedList
- Linear structure with nodes linked via pointers.
- No built-in support; needs a custom class.
- Useful for efficient insert/delete in middle.

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

### 7. HashMap / HashSet
- Python’s built-in `dict` and `set` are hash-based.
- Constant time lookup (`O(1)` average).
- Used for frequency counting, fast membership checks.

```python
my_map = {'a': 1}
my_set = set([1, 2, 3])
```

### 8. Trie (Prefix Tree)
- Tree where each path is a prefix.
- Best for autocomplete, prefix search, word dictionary.
- Custom class needed.

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False
```

### 9. Disjoint Set / Union-Find
- Structure to keep track of connected components.
- Used in Kruskal’s algorithm, cycle detection, DSU.
- You write your own logic using parent and rank arrays.

```python
parent = [i for i in range(n)]

def find(x):
    if parent[x] != x:
        parent[x] = find(parent[x])
    return parent[x]

def union(x, y):
    parent[find(x)] = find(y)
```



