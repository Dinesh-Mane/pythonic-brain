## 1. What’s the output and why? (Mutability Trap)
```python
t = ([1, 2], 3)
t[0].append(99)
print(t)
```
### **Answer:**
```python
([1, 2, 99], 3)
```
> Tuple is immutable, but its contents may be mutable.  
> `t[0]` is a list — lists are mutable.

## 2. Can two different tuples have the same hash?
```python
print(hash((1, 2)))
print(hash((1.0, 2.0)))
```
### **Answer:** Yes, they might produce the same hash (depends on implementation), because 1 == 1.0.
`(1, 2)` and `(1.0, 2.0)` look different but:
- `1 == 1.0` → True
- Python's hashing logic treats numeric equivalents equally.

## 3. What’s the output and why? (Tuple Packing/Unpacking)
```python
a = 1, 2, 3
b = (1, 2, 3)
print(a == b, a is b)
```
### **Answer:**  
```python
True False
```
- `a` → tuple due to comma: (1, 2, 3)
- `b` → explicit tuple: (1, 2, 3)
- `a == b` → True: values are equal.
- `a is b` → False: different memory objects.

## 4. Can you sort a list of tuples by second element, descending?
```python
data = [(1, 2), (3, 1), (5, 0)]
# Sort by second element descending
```
### **Answer:**
```python
data.sort(key=lambda x: x[1], reverse=True)
print(data)   # [(1, 2), (3, 1), (5, 0)]
```

## 5. How to break a tie in tuple sort?
```python
data = [(2, 'b'), (2, 'a'), (1, 'c')]
# Sort by first, break tie using second
```
### **Answer:**
```python
data.sort()  # Tuple comparison is lexicographic by default
```
Python sorts tuples lexicographically  
Sort order: Compare first elements → if same, then second  
```python
(1, 'c') < (2, 'a') < (2, 'b')
```

## 6. What’s the output of this comparison?
```python
print((1, 2) < (1, 2, 0))
```
### **Answer:** `True`
Tuple comparison is element-wise → shorter one is smaller if all elements are equal.  
Element-by-element comparison:  
- `1 == 1`
- `2 == 2`
- Left side ends → Python considers shorter tuple as smaller

## 7. Tuple with mutable default argument in function
```python
def foo(t = ([],)):
    t[0].append(1)
    return t

print(foo())
print(foo())
```
### **Answer:**
```python
([1],)
([1, 1],)
```
Even though the tuple is immutable, its list content is shared across calls!  
> Lists are shared across calls (default arguments are only created once)  
> So appending affects same list every time

## 8. Can tuple keys in a dictionary simulate a matrix?
```python
matrix = {}
matrix[(1, 2)] = 5
matrix[(2, 1)] = 6

print(matrix[(1, 2)])
```
### **Answer:**  Yes! Tuples are used as (row, col) keys — like a 2D array.
> You can use tuples as keys in a dict because they're immutable  
> Great for 2D coordinates
```python
matrix[(x, y)] → is like accessing grid[x][y]
```

## 9. Tuple in a set: Will this work?
```python
s = set()
s.add(([1, 2],))  # Tuple of list
```
### **Answer:** TypeError: unhashable type: 'list'
Even though it’s a tuple, the inner list is mutable, hence unhashable → so the full tuple becomes unhashable

## 10. What's wrong with this visited set?
```python
visited = set()
visited.add((x, y))  # x and y are lists
```
### **Answer:** TypeError
Reason: You cannot use a list inside a tuple in a set:
```python
( [1], 2 ) ❌  → because [1] is unhashable
visited.add((x, y))  # If x or y is a list → ❌ Error
visited.add((x, y))  # ✅ only if x and y are ints or strings
```

## 11. Which is faster: list or tuple access? Why?
Tuple access is slightly faster (about 10–15%) because:  
Tuples are immutable → no dynamic resizing, no method overhead.

## 12. Tuple Unpacking/Destructuring in Loops — What’s going on?
```python
data = [(1, 2), (3, 4), (5, 6)]
for x, y in data:
    print(x + y)
```
### **Answer:** 
```python
3
7
11
```
Explanation: This is tuple unpacking inside a loop.  
(1,2) → x=1, y=2 → 3  
(3,4) → x=3, y=4 → 7  

## 13. Can you reverse a tuple?
### **Answer:** Yes! Same slicing logic as lists
```python
t = (1, 2, 3)
t[::-1]  # (3, 2, 1)
```

## 14. Tuple vs NamedTuple vs dataclass — when do you use what?
```python
s = set()
s.add(([1, 2],))  # Tuple of list
```
### **Answer:** 
- Use `tuple`: Lightweight, simple grouping
- Use `namedtuple`: When you want readability (`.x, .y`)
- Use `dataclas`: When you want mutability, default values, and type checking

| Feature         | `tuple` | `namedtuple` | `dataclass`    |
| --------------- | ------- | ------------ | -------------- |
| Immutable       | ✅       | ✅            | ❌ (by default) |
| Readable fields | ❌       | ✅ (`.x`)     | ✅              |
| Type hints      | ❌       | ❌            | ✅              |
| Defaults        | ❌       | ❌            | ✅              |

## 14. Tuple vs NamedTuple vs dataclass — when do you use what?
### **Answer:** 
- Use `tuple`: Lightweight, simple grouping
- Use `namedtuple`: When you want readability (`.x, .y`)
- Use `dataclas`: When you want mutability, default values, and type checking


## 15. Use Case: Avoiding Duplicate Paths in Backtracking
```python
path = []
res = set()

def dfs(i):
    if i == n:
        res.add(tuple(path))
        return

    for choice in options:
        path.append(choice)
        dfs(i + 1)
        path.pop()
```
### **Answer:** 
Here `tuple(path)` is used because:
- `list` is unhashable
- We want to avoid storing the same path multiple times

>  Needed because list is unhashable → cannot go in a set  
> Use tuple(path) to store unique combinations  


## 16. Tuple-Based Key for Caching with Multiple Parameters
```python
from functools import lru_cache

@lru_cache(None)
def solve(i, j, k):
    ...
```
Internally, Python uses a tuple (i, j, k) as the key.  
Tuple key makes memoization fast and reliable  

## 17. Tuple as Immutable Coordinates in DFS on a Grid
```python
def dfs(r, c):
    if (r, c) in visited:
        return
    visited.add((r, c))
```
Here, `(r, c)` acts like a unique fingerprint of a cell.  
Unique and immutable → perfect for tracking visited nodes  

## 18. Tuple of Tuples — Can You Do This?
```python
combo = ((1, 2), (3, 4))
print(combo in set([((1, 2), (3, 4))]))
```
Ans: Yes — tuple of tuples is hashable  
Valid because inner tuples are also immutable  

## 19. Compare memory usage of tuple vs list
```python
import sys
print(sys.getsizeof((1, 2, 3)))   # Smaller
print(sys.getsizeof([1, 2, 3]))   # Bigger
sys.getsizeof(tuple) < sys.getsizeof(list)  # ✅ True
```

## 20. Tuple with generator — What’s the result?
```python
t = tuple(x*x for x in range(3))
print(t)
```
Output:
```python
(0, 1, 4)
```
