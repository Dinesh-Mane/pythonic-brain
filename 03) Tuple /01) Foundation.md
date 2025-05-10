# What is a Tuple?
A tuple is an **ordered**, **immutable** collection of elements in Python.
```python
t = (1, 2, 3)
```
### Key Features:
| Feature       | Explanation                                                                    |
| ------------- | ------------------------------------------------------------------------------ |
| Ordered       | Elements maintain their insertion order (from Python 3.6+)                     |
| Immutable     | Cannot change values after creation                                            |
| Heterogeneous | Can store mixed data types                                                     |
| Hashable      | Can be used as keys in a dictionary (if all elements inside are also hashable) |

### Use tuples when:
- You want to ensure data cannot be modified.
- You want to use it as a key in a dictionary or element in a `set`.
> Heavily used in DSA problems: grid traversal, heaps, memoization, graphs, etc.

## Tuple vs List
| Feature     | List   | Tuple                     |
| ----------- | ------ | ------------------------- |
| Mutable     | ✅ Yes  | ❌ No                      |
| Hashable    | ❌ No   | ✅ Yes (if immutable)      |
| Performance | Slower | Faster (more lightweight) |
| Syntax      | `[]`   | `()`                      |

| Operation       | List   | Tuple                            |
| --------------- | ------ | -------------------------------- |
| Creation time   | Slower | Faster                           |
| Memory usage    | Higher | Lower                            |
| Use as dict key | ❌ No   | ✅ Yes (if contents are hashable) |

# Tuple Operations

## 1. Creating Tuples
### A. Basic Tuple
```python
t = (1, 2, 3)
print(t)  # (1, 2, 3)
```
### B. Tuple without parentheses
```python
t = 1, 2, 3    # Still a tuple!
print(t)  # (1, 2, 3)
```
### C. Single Element Tuple
```python
t = (5,)     # Correct
x = (5)      # NOT a tuple, just int
print(type(t))  # <class 'tuple'>
```

## 2. Accessing Elements
### A. Indexing
```python
t = ('a', 'b', 'c')
print(t[0])   # 'a'
print(t[-1])  # 'c'
```

### C. Slicing
```python
t = (10, 20, 30, 40)
print(t[1:3])  # (20, 30)
print(t[:2])   # (10, 20)
```

## 3. Length of Tuple
```python
t = (1, 2, 3)
print(len(t))  # 3
```

## 4. Tuple Concatenation
```python
t1 = (1, 2)
t2 = (3, 4)
t3 = t1 + t2
print(t3)  # (1, 2, 3, 4)
```

## 5. Tuple Repetition
```python
t = (1, 2)
print(t * 3)  # (1, 2, 1, 2, 1, 2)
```

## 6. Membership Testing
```python
t = (1, 2, 3)
print(2 in t)     # True
print(5 not in t) # True
```

## 7. Iterating Over Tuple
```python
t = ('a', 'b', 'c')
for item in t:
    print(item)
```

## 8. Tuple Unpacking
### A. Basic Unpacking
```python
t = (1, 2, 3)
a, b, c = t
print(a, b, c)  # 1 2 3
```
### B. Extended Unpacking
```python
t = (1, 2, 3, 4, 5)
a, *b, c = t
print(a, b, c)  # 1 [2, 3, 4] 5
```


## 9. Nested Tuples
```python
t = ((1, 2), (3, 4))
print(t[1][0])  # 3
```

## 10. Using `tuple()` Constructor
```python
l = [1, 2, 3]
t = tuple(l)
print(t)  # (1, 2, 3)
```

## 11. Count Occurrences
```python
t = (1, 2, 2, 3, 2)
print(t.count(2))  # 3
```


## 12. Find Index of Value
```python
t = (5, 10, 15, 10)
print(t.index(10))  # 1 (first occurrence)
```

## 13. Use as Dictionary Keys
```python
d = {}
key = (1, 2)
d[key] = "value"
print(d[(1, 2)])  # value
```

## 14. Min, Max, Sum
```python
t = (5, 1, 8, 3)
print(min(t))  # 1
print(max(t))  # 8
print(sum(t))  # 17
```

## 15. Sorting a Tuple
Tuples are immutable, so you sort by converting to a list:
```python
t = (3, 1, 2)
sorted_t = tuple(sorted(t))
print(sorted_t)  # (1, 2, 3)
```
## 16. Tuple Comprehension?
There's no direct tuple comprehension, but use generator expression:
```python
t = tuple(x**2 for x in range(4))
print(t)  # (0, 1, 4, 9)
```

## 17. Tuple Inside List / List Inside Tuple
```python
# Tuple inside list
tl = [(1, 2), (3, 4)]

# List inside tuple (mutable inside immutable)
lt = ([1, 2], [3, 4])
lt[0][0] = 99
print(lt)  # ([99, 2], [3, 4])
```
**Note: Even though the tuple itself is immutable, it can hold mutable items**  
So tuple is shallow immutable, but its **contents can be mutable!**  

## 18. Tuple with `*args` in Functions
```python
def add(*args):
    print(args)

add(1, 2, 3)  # args = (1, 2, 3)
```


## 19. Tuple with `enumerate()`
```python
t = ('a', 'b', 'c')
for index, value in enumerate(t):
    print(index, value)
```

## 20. Tuple with `zip()`
```python
t = (5, 10, 15, 10)
print(t.index(10))  # 1 (first occurrence)
```

## 21. Tuple with Heap (Priority Queue)
```python
import heapq
heap = []
heapq.heappush(heap, (2, 'task2'))
heapq.heappush(heap, (1, 'task1'))
print(heapq.heappop(heap))  # (1, 'task1')
```

## Summary : 
| Operation   | Syntax / Function   | Notes                    |
| ----------- | ------------------- | ------------------------ |
| Creation    | `(1, 2)`, `tuple()` | Immutable                |
| Indexing    | `t[0]`, `t[-1]`     | Read access              |
| Slicing     | `t[1:3]`            | Returns tuple            |
| Length      | `len(t)`            | Size                     |
| Count       | `t.count(x)`        | Frequency                |
| Index       | `t.index(x)`        | First index              |
| Concatenate | `t1 + t2`           | New tuple                |
| Repeat      | `t * 3`             | Repetition               |
| Membership  | `x in t`            | True/False               |
| Iteration   | `for i in t`        | Loop                     |
| Min/Max/Sum | `min(t)` etc.       | Only for numeric tuples  |
| Sorting     | `sorted(t)` → tuple | Returns new sorted tuple |
| Use as key  | `d[(a,b)] = val`    | Tuple must be hashable   |
| Packing     | `t = a, b, c`       | No parentheses needed    |
| Unpacking   | `a, b, c = t`       | Even extended form       |
| Heap Use    | `heapq` with tuples | Used in Dijkstra, etc.   |


## When Are Tuples Used in DSA?
### 1. Coordinate Pairs – `(x, y)` Points
**Use Case:** Storing 2D grid positions like in maze, matrix, or BFS/DFS traversal.
```python
points = [(0, 0), (1, 2), (-1, 3)]
```
> Each tuple is a coordinate: `(row, col)`

**Example: BFS in a Matrix**
```python
from collections import deque

grid = [
    [0, 1],
    [0, 0]
]

visited = set()
q = deque()
q.append((0, 0))  # Start from top-left

while q:
    r, c = q.popleft()
    if (r, c) in visited:
        continue
    visited.add((r, c))
    
    # Go right and down
    for dr, dc in [(0,1), (1,0)]:
        nr, nc = r+dr, c+dc
        if 0 <= nr < 2 and 0 <= nc < 2 and grid[nr][nc] == 0:
            q.append((nr, nc))
```
> Why tuple?  
> Coordinates like `(r, c)` are immutable  
> Can be added to `set` (which needs hashable types)  

### 2. Graph Edges as Tuples
**Use Case:** Representing edges of a graph — useful in DFS, BFS, Dijkstra, MST, etc.
```python
edges = [(u, v) for u in range(n) for v in graph[u]]
```
> This creates a list of (from, to) edges.

**Example: Undirected Graph**
```python
graph = {
    0: [1, 2],
    1: [0, 3],
    2: [0],
    3: [1]
}

edges = []

for u in graph:
    for v in graph[u]:
        edges.append((u, v))

print(edges)
# [(0, 1), (0, 2), (1, 0), (1, 3), (2, 0), (3, 1)]
```
> These `(u, v)` edges can be used in algorithms like:  
> Union-Find (Disjoint Set)  
> Kruskal’s Algorithm  

### 3. Tuples as Memoization Keys
**Use Case:**   
When using DP + recursion, you cache results based on function parameters.  
Tuples are hashable → can be used as `dict` keys.  

**Example: Recursive DP with Memoization** 
```python
dp = {}

def solve(i, j):
    if (i, j) in dp:
        return dp[(i, j)]
    
    if i == 0 or j == 0:
        result = 0
    else:
        result = solve(i-1, j) + solve(i, j-1)

    dp[(i, j)] = result
    return result
```
> Tuple (i, j) is used as a key to memoize state.  
> Cannot use lists as dict keys since they are mutable.  
> Tuples guarantee fixed structure and immutability.  

### 4. Set of Tuples – Removing Duplicates
**Use Case:** When you need unique combinations or visited states, you can store tuples in set.

**Example: Unique Pairs**
```python
pairs = [(1, 2), (2, 1), (1, 2), (3, 4)]
unique = set(pairs)

print(unique)  # {(1, 2), (2, 1), (3, 4)}
```
> Each element in the set is a tuple, and duplicates are removed automatically.

If you use lists instead:
```python
pairs = [[1, 2], [1, 2]]
set(pairs)  # ❌ TypeError: unhashable type: 'list'
```
**Example: Keeping Track of Visited Coordinates**
```python
visited = set()
visited.add((0, 0))  # OK
visited.add((0, 0))  # Won’t add again
```
> Useful in:  
> Flood fill  
> Maze traversal  
> Knight moves / BFS  

