# `enumerate()` function
`enumerate()` is a built-in function used to loop through an iterable (like list, tuple, string, etc.) and keep track of the index automatically.

Syntax:
```python
enumerate(iterable, start=0)
```
Parameters:
| Parameter  | Description                                        |
| ---------- | -------------------------------------------------- |
| `iterable` | Any iterable object like list, string, tuple, etc. |
| `start`    | (Optional) The starting index. Default is `0`.     |

## Basic Example
```python
fruits = ['apple', 'banana', 'cherry']

for index, value in enumerate(fruits):
    print(index, value)
```
Output:
```
0 apple
1 banana
2 cherry
```
**`enumerate()` gives you:**
1. `index` (starting from 0 by default)
2. `value` (from the iterable)


## Example with Custom Start Index
```python
fruits = ['apple', 'banana', 'cherry']

for i, fruit in enumerate(fruits, start=1):
    print(f"{i}. {fruit}")
```
Output:
```
1. apple
2. banana
3. cherry
```
You can customize the index using `start=` parameter.

## Example: Convert Enumerate to List
```python
colors = ['red', 'green', 'blue']
enum_obj = enumerate(colors)

print(list(enum_obj))
```
Output:
```css
[(0, 'red'), (1, 'green'), (2, 'blue')]
```
You can directly convert the `enumerate` object to a list of `(index, value)` tuples.

## Example: Enumerate Over String
```python
word = "cat"

for index, letter in enumerate(word):
    print(index, letter)
```
Output:
```css
0 c
1 a
2 t
```
Works with any iterable, including strings


## Example: Enumerate Over Tuple
```python
items = ('pen', 'book', 'ink')

for i, item in enumerate(items):
    print(f"Index: {i}, Item: {item}")
```
Output:
```css
Index: 0, Item: pen
Index: 1, Item: book
Index: 2, Item: ink
```


## Example: Nested Enumerate Loop
```python
matrix = [[1, 2], [3, 4], [5, 6]]

for row_idx, row in enumerate(matrix):
    for col_idx, value in enumerate(row):
        print(f"Row {row_idx}, Col {col_idx}: {value}")
```
Output:
```css
Row 0, Col 0: 1
Row 0, Col 1: 2
Row 1, Col 0: 3
Row 1, Col 1: 4
Row 2, Col 0: 5
Row 2, Col 1: 6
```
Useful in 2D data structures.

## Example: Filter List with Enumerate
```python
nums = [10, 20, 30, 40, 50]

# Get index of values > 25
for i, val in enumerate(nums):
    if val > 25:
        print(f"Index: {i}, Value: {val}")
```
Output:
```css
2 30
3 40
4 50
```


## Enumerate with `zip()`
```python
names = ['Alice', 'Bob']
scores = [80, 90]

for i, (name, score) in enumerate(zip(names, scores), start=1):
    print(f"{i}. {name} scored {score}")
```
Output:
```css
1. Alice scored 80
2. Bob scored 90
```
Combines both `zip()` and `enumerate()` for powerful data processing

## Unpacking Enumerate Object
```python
x = ['a', 'b', 'c']
indexed = list(enumerate(x))

for item in indexed:
    print(item)
```
Output:
```css
(0, 'a')
(1, 'b')
(2, 'c')
```
Each tuple can be unpacked as `(index, value)`


## Enumerate in List Comprehension
```python
colors = ['red', 'green', 'blue']
upper_colors = [f"{i}: {color.upper()}" for i, color in enumerate(colors)]

print(upper_colors)
```
Output:
```css
['0: RED', '1: GREEN', '2: BLUE']
```
Each tuple can be unpacked as `(index, value)`

# Things to Remember
| Point                                              | Explanation                                         |
| -------------------------------------------------- | --------------------------------------------------- |
| `enumerate()` returns an iterator                  | Not a list — convert with `list()` if needed.       |
| Works with any iterable                            | list, tuple, set, string, generator, etc.           |
| Avoid modifying iterable inside `enumerate()` loop | It may cause index mismatch or unexpected behavior. |
| Start parameter is optional                        | Default is `0`, but can be changed.                 |

