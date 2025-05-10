# All Common Output Scenarios
## SCENARIO 1: Print a Single Value
Most basic output
Input:
```python
x = 10
```
Output:
```python
10
```
Code:
```python
print(x)
```
## SCENARIO 2: Print Space-Separated Values
Problem type: Output multiple values in one line
Input:
```python
a, b, c = 1, 2, 3
```
Output:
```python
1 2 3
```
Code:
```python
print(a, b, c)
```
> Default separator in print() is space.

## SCENARIO 3: Print Without Space (like comma-separated or joined string)
You control the separator
Input:
```python
nums = [1, 2, 3, 4]
```
Output:
```python
1-2-3-4
```
Code:
```python
print("-".join(map(str, nums))))
```

## SCENARIO 4: Print Without Newline (like all in one line)
Used in grid printing, simulations  
Output:
```python
ABC
```
Code:
```python
print("A", end="")
print("B", end="")
print("C")
```

## SCENARIO 5: Output Matrix/Grid Format (row by row)
Very common for 2D problems  
Input:
```python
matrix = [[1, 2], [3, 4]]
```
Output:
```python
1 2
3 4
```
Code:
```python
for row in matrix:
    print(*row)
```

## SCENARIO 6: Print List Elements in One Line
Output an entire list cleanly  
Output:
```python
10 20 30 40
```
Code:
```python
arr = [10, 20, 30, 40]
print(*arr)
```
`*` operator unpacks the list into print() arguments.

## SCENARIO 7: Formatted Output
Used for printing float values, padding, etc.  
Output:
```python
Pi is 3.14
```
Code:
```python
pi = 3.14159
print("Pi is {:.2f}".format(pi))
```
OR Code (f-string):
```python
print(f"Pi is {pi:.2f}")
```

## SCENARIO 8: Yes/No or True/False Output
Common in Leetcode / logic-based problems  
Code:
```python
print("YES" if condition else "NO")
```

## SCENARIO 9: Output Multiple Test Case Results
For `T` test cases, output must be line by line  
Output:
```python
Case #1: 12
Case #2: 24
```
Code:
```python
T = int(input())
for i in range(1, T + 1):
    ans = i * 12
    print(f"Case #{i}: {ans}")
```

## SCENARIO 10: Output Dictionary or JSON-like Data
Print in formatted way
```python
import json
data = {"a": 1, "b": 2}
print(json.dumps(data))  # {"a": 1, "b": 2}
```

## SCENARIO 11: Print All Outputs at Once (for speed)
Use in CP when `print()` is slow in loop
```python
output = []
for i in range(5):
    output.append(str(i * i))
print("\n".join(output))
```

## SCENARIO 12: Output Characters Without Spaces
Useful for grid/maze/board printing
```python
arr = ['a', 'b', 'c']
print("".join(arr))  # abc
```

## SCENARIO 13: Custom Delimiters in Output
When output is comma/pipe/tab separated
```python
nums = [1, 2, 3]
print(",".join(map(str, nums)))  # 1,2,3
```

## SCENARIO 14: Print on Same Line (in loop)
```python
for i in range(5):
    print(i, end=" ")  # 0 1 2 3 4
```

## SCENARIO 15: Debug/Print to `stderr`
Debug without affecting real output
```python
import sys
print("Debugging here", file=sys.stderr)
```

