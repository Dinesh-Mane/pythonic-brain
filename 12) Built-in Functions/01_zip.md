# `zip()` function
The `zip()` function in Python is a powerful built-in that is commonly used for combining iterables. It returns an iterator of tuples, where the i-th tuple contains the i-th element from each of the input iterables.
Syntax:
```python
zip(iterable1, iterable2, ..., iterableN)
```
- iterable1, iterable2, ..., iterableN: These can be lists, tuples, strings, sets, or any iterable.
- Returns: an iterator of tuples.

## Basic Working Principle:
It pairs items element-wise from all input iterables.
> Stops at the shortest iterable to avoid IndexError


## Example 1: Zipping Two Lists
```python
names = ['Alice', 'Bob', 'Charlie']
scores = [85, 90, 78]

zipped = zip(names, scores)
print(list(zipped))
```
Output:
```css
[('Alice', 85), ('Bob', 90), ('Charlie', 78)]
```
Alice paired with 85, and so on.


## Example 2: Zipping Lists of Unequal Lengths
```python
a = [1, 2, 3]
b = ['a', 'b']

print(list(zip(a, b)))
```
Output:
```css
[(1, 'a'), (2, 'b')]
```
`zip()` stops at the shortest iterable


## Example 3: Using zip() in a Loop
```python
names = ['Tom', 'Jerry', 'Spike']
ages = [5, 6, 7]

for name, age in zip(names, ages):
    print(f"{name} is {age} years old.")
```
Output:
```css
Tom is 5 years old.
Jerry is 6 years old.
Spike is 7 years old.
```


## Example 4: Zipping Three or More Iterables
```python
roll_numbers = [101, 102, 103]
names = ['Amit', 'Pooja', 'Ravi']
marks = [80, 90, 85]

for roll, name, mark in zip(roll_numbers, names, marks):
    print(roll, name, mark)
```
Output:
```css
101 Amit 80
102 Pooja 90
103 Ravi 85
```


## Example 5: Unzipping (Reverse of zip)
Unpacking zipped values
```python
zipped = [('a', 1), ('b', 2), ('c', 3)]
letters, numbers = zip(*zipped)

print(letters)
print(numbers)
```
Output:
```css
('a', 'b', 'c')
(1, 2, 3)
```
`*zipped` unpacks the zipped list of tuples


## Example 6: zip() with Strings
Unpacking zipped values
```python
s1 = 'abc'
s2 = '123'

print(list(zip(s1, s2)))
```
Output:
```css
[('a', '1'), ('b', '2'), ('c', '3')]
```
Works with any iterable, including strings


## Example 7: zip() with Sets (unordered)
```python
set1 = {1, 2, 3}
set2 = {'a', 'b', 'c'}

print(list(zip(set1, set2)))
```
Output: (Order not guaranteed due to set behavior)
```css
[(1, 'b'), (2, 'a'), (3, 'c')]  # may vary
```
Sets are unordered → output can be inconsistent.

## Example 8: zip() with zip_longest (to handle unequal lengths)
`zip()` ignores extra values, but `itertools.zip_longest` handles that.
```python
from itertools import zip_longest

a = [1, 2]
b = ['x', 'y', 'z']

result = list(zip_longest(a, b, fillvalue='NA'))
print(result)
```
Output:
```css
[(1, 'x'), (2, 'y'), ('NA', 'z')]
```


## Example 9: Dictionary creation with zip()
```python
keys = ['id', 'name', 'age']
values = [1, 'John', 30]

data = dict(zip(keys, values))
print(data)
```
Output:
```css
{'id': 1, 'name': 'John', 'age': 30}
```
Common usage in data mapping.


## Example 10: Use with `enumerate()` and `zip()`
```python
list1 = ['a', 'b', 'c']
list2 = [10, 20, 30]

for index, (x, y) in enumerate(zip(list1, list2)):
    print(index, x, y)
```
Output:
```css
0 a 10
1 b 20
2 c 30
```


# Important Notes:
| Behavior                     | Explanation                                                                              |
| ---------------------------- | ---------------------------------------------------------------------------------------- |
| **Lazy Evaluation**          | `zip()` returns an **iterator**, not a list. You need to convert using `list()` or loop. |
| **Shortest Iterable Wins**   | Stops zipping when the **shortest iterable ends**.                                       |
| **Unpacking with `*`**       | Can **unzip** or separate zipped tuples using unpacking.                                 |
| **Works with All Iterables** | Lists, tuples, sets, strings, etc.                                                       |
| **Use `zip_longest`**        | When you need to **fill missing values** for unequal lengths.                            |
