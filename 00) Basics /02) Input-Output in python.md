# All Common Input Scenarios
## SCENARIO 1: Single Integer Input
Problem type: When you are given just one number as input.
```python
5
```
### Method 1: `int(input())`
```python
n = int(input())
```
## SCENARIO 2: Space-Separated Integers
Problem type: Multiple values given in one line separated by space.
```python
5 7 9
```
### Method 1: Using map
```python
a, b, c = map(int, input().split())
```
### Method 2: Read into a list
```python
arr = list(map(int, input().split()))
```

## SCENARIO 3: Multiple Lines of Input (Fixed number of lines)
Problem type: Each line contains a new value. You know beforehand how many lines you'll receive.
```python
3
10
20
30
```
### Method : 
```python
n = int(input())
arr = []
for _ in range(n):
    arr.append(int(input()))
```

## SCENARIO 4: Matrix Input (2D array)
Problem type: Multiple rows, each with space-separated values.
```python
3 3
1 2 3
4 5 6
7 8 9
```
### Method : 
```python
rows, cols = map(int, input().split())
matrix = []
for _ in range(rows):
    matrix.append(list(map(int, input().split())))
```

## SCENARIO 5: Unknown number of lines (EOF input)
Problem type: Input ends when there is no more data.
```python
5
10
3
8
```
### Method: try-except (for CP platforms)
```python
import sys
for line in sys.stdin:
    print(int(line))  # or store it in a list
```

## SCENARIO 6: Test Cases (T lines of input)
Problem type: You’re told how many test cases you’ll receive.
```python
2
3 5
1 2
```
### Method:
```python
T = int(input())
for _ in range(T):
    a, b = map(int, input().split())
```

## SCENARIO 7: Characters as Input
Problem type: You get one or more characters, space-separated or not.
### Example 1 (No space):
```python
abc
```
### Method: 
```python
chars = list(input())  # ['a', 'b', 'c']
```

### Example 2 (Space-separated):
```python
a b c
```
### Method: 
```python
chars = input().split()  # ['a', 'b', 'c']
```

## SCENARIO 8: Tuples as Input
Problem type: Tuple of values is given in one line.
```python
1,2,3
```
### Method:
```python
t = tuple(map(int, input().split(',')))
```

## SCENARIO 9: Dictionary-like Input
Problem type: Key-value pairs in multiple lines.
```python
3
name Alice
age 25
city Mumbai
```
### Method:
```python
n = int(input())
d = {}
for _ in range(n):
    key, value = input().split()
    d[key] = value
```

## SCENARIO 10: Graph Input (Edges List)
Problem type: Undirected or directed graph given by list of edges.
```python
5 4
1 2
1 3
3 4
2 5
```
### Method:
```python
n, e = map(int, input().split())
edges = []
for _ in range(e):
    u, v = map(int, input().split())
    edges.append((u, v))
```

## SCENARIO 11: String with Delimiters
Problem type: Input is comma/semicolon-separated string.
```python
10,20,30
```
### Method:
```python
arr = list(map(int, input().split(',')))
```

## SCENARIO 12: Input via `sys.stdin` for large data
Problem type: Competitive programming where `input()` is slow.
### Method:
```python
import sys
input = sys.stdin.readline
n = int(input())
```

## SCENARIO 13: Flattened Matrix in One Line
Problem type: All matrix values in one line (e.g., Leetcode)
```python
1 2 3 4 5 6 7 8 9
```
### Method:
```python
flat = list(map(int, input().split()))
rows, cols = 3, 3
matrix = [flat[i * cols: (i + 1) * cols] for i in range(rows)]
```

## SCENARIO 14: JSON-like or Nested Input
Problem Type: Sometimes, coding platforms or company-specific coding rounds give you complex inputs in the form of JSON, i.e., dictionaries, lists, or a mix of both — all in one line or multiple lines.
### Basic JSON/Nested Structure:
```python
{"name": "Alice", "age": 25, "skills": ["Python", "AWS", "Docker"]}
```
### Method:
```python
import json

data = json.loads(input())
print(data["name"])         # Alice
print(data["skills"][0])    # Python
```
> `json.loads()` = convert string to Python dictionary/list.

EXAMPLE 1: List of Dictionaries
```python
[{"id": 1, "val": 10}, {"id": 2, "val": 20}]
```
### Method:
```python
import json

data = json.loads(input())
for item in data:
    print(item["id"], item["val"])
```

### EXAMPLE 2: Dictionary with Nested List of Tuples
```python
{"nodes": [[1, 2], [2, 3], [4, 5]]}
```
### Method:
```python
import json

graph = json.loads(input())
for u, v in graph["nodes"]:
    print(f"Edge from {u} to {v}")
```

### EXAMPLE 3: Nested Dictionary
```python
{"user": {"id": 101, "details": {"name": "John", "city": "Pune"}}}
```
### Method:
```python
import json

data = json.loads(input())
print(data["user"]["details"]["city"])  # Pune
```

### EXAMPLE 4: Tree-like Structure
```python
{"val": 1, "left": {"val": 2}, "right": {"val": 3}}
```
This simulates a binary tree node.

### Method:
```python
import json

node = json.loads(input())
print(node["val"])             # 1
print(node["left"]["val"])     # 2
print(node["right"]["val"])    # 3
```
> Note: Only use `json.loads()` if input is a valid JSON string
