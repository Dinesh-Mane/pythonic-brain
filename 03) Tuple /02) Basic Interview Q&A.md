# Basic Python Tuple Questions

## 1. What is a tuple in Python? How is it different from a list?
- Tuple: Ordered, immutable collection of elements.
- Difference: Tuples cannot be modified after creation. Lists are mutable.

## 2. How do you create a tuple with only one element?
```python
t = (5,)
```
> Without the comma, Python treats it as an int.

## 3. Can a tuple contain mutable elements?
Yes. A tuple itself is immutable, but it can contain mutable elements like lists.
```python
t = ([1, 2], 3)
t[0][0] = 99  # Valid
```

## 4. Can you modify a tuple after creation?
No – you can’t change, add, or delete elements from a tuple directly.

## 5. How do you access tuple elements?
Using indexing and slicing, like lists.
```python
t = (1, 2, 3)
print(t[1])  # 2
```

## 6. How do you concatenate or repeat tuples?
```python
t1 + t2     # Concatenation
t1 * 3      # Repetition
```

## 7. How do you count elements or find an element's index in a tuple?
```python
t.count(x), t.index(x)
```

## 8. Why are tuples used as dictionary keys or in sets?
Because they are immutable and hashable, unlike lists.

## 9. Explain how you would use a tuple in a BFS/DFS problem.
To represent a coordinate or a visited node:
```python
visited = set()
queue.append((r, c))
```

## 10. How are tuples used in memoization?
Memoization caches states using tuples as keys:
```python
dp = {}
def f(i, j):
    if (i, j) in dp:
        return dp[(i, j)]
```

## 11. What is tuple unpacking?
Assigning tuple elements to variables in one line.
```python
a, b = (1, 2)
```

## 12. What is extended unpacking in Python?
```python
a, *b, c = (1, 2, 3, 4)
# a = 1, b = [2, 3], c = 4
```

## 13. What will be the output of this code?
```python
a = (1, 2)
b = (1, 2)
print(a is b)
```
Answer: `False` (two different memory locations)

## 14. How would you use a tuple in sorting custom data?
```python
data = [(2, 'b'), (1, 'a'), (2, 'a')]
data.sort()  # Sorted by first, then second
```

## 15. How are tuples used in priority queues (heapq)?
```python
import heapq
heapq.heappush(heap, (priority, task))
```
Tuple is used so Python compares based on first item (`priority`).

## 16. Find the most common tuple from a list of tuples.
```python
from collections import Counter
tuples = [(1,2), (2,3), (1,2)]
most_common = Counter(tuples).most_common(1)
print(most_common)  # [((1, 2), 2)]
```

## 17. Remove duplicate tuples from a list.
```python
unique = list(set(tuples))
```

## 18. How to convert a list of tuples to a dictionary?
```python
t = [(1, 'a'), (2, 'b')]
d = dict(t)
```

## 19. Convert a dictionary to a list of tuples (items).
```python
d = {'a': 1, 'b': 2}
list(d.items())  # [('a', 1), ('b', 2)]
```

## 20. Can a tuple contain itself?
Yes (but rare):
```python
t = (1,)
t = (t,)
print(t)  # ((...),)
```

## 21. What happens if you try to modify a tuple directly?
```python
t = (1, 2)
t[0] = 5  # ❌ TypeError: 'tuple' object does not support item assignment
```















































