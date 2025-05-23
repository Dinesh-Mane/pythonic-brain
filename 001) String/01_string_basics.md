# String
A string in Python is an immutable ordered sequence of characters.
- **Immutable**: Once a string is created, it cannot be changed.
- **Ordered:** Characters in a string have a specific index starting from 0.

## String Creation:
```python
# Using single quotes
s1 = 'Hello'

# Using double quotes
s2 = "World"

# Using triple quotes (multi-line string)
s3 = '''This is 
a multi-line 
string'''

print(s1)
print(s2)
print(s3)
```

# String Operations
## 1. Indexing
Accessing individual characters by position.
```python
s = "Python"
print(s[0])    # P
print(s[5])    # n
print(s[-1])   # n (last character)
```
> Tip: Use negative indexing to access from the end.

## 2. Slicing
Extract a substring using `s[start:end:step]`
```python
s = "Python"
print(s[1:4])   # yth
print(s[:3])    # Pyt
print(s[::2])   # Pto
```
> `[start, end)` -> start wala index included asto, pn end wala nhi
> Use slicing for pattern problems or substring manipulations.

## 3. Length
```python
s = "DevOps"
print(len(s))   # 6
```
## 4. Concatenation
### 4A. Using `+` Operator
```python
print("Hello" + " World")  # Hello World
```
OR
```python
s1 = "Hello"
s2 = "World"
result = s1 + " " + s2
print(result)  # Hello World
```
### 4B. Using `+=` (Augmented Assignment)
The most basic and direct way.
```python
print("Hello" + " World")  # Hello World
```
OR
```python
s1 = "Hello"
s2 = "World"
result = s1 + " " + s2
print(result)  # Hello World
```
### 4C. Using `join()` method (Most Efficient)
Adds to the existing string variable.
```python
words = ["Hello", "World", "from", "Python"]
result = " ".join(words)
print(result)  # Hello World from Python
```
Use when:
- Concatenating many strings (especially in loops).
- More performant than `+`

### 4D. Using f-string (Formatted String Literal)
Python 3.6+ way of building strings.
```python
name = "Alice"
age = 30
print(f"My name is {name} and I am {age} years old.")
```
> Clean and readable way of combining variables into strings.

### 4E. Using `%` operator (Old-style formatting)
```python
name = "Charlie"
print("Hello %s!" % name)  # Hello Charlie!
```
> Obsolete in modern code, used mostly in legacy projects.

### 4F. Using List + join (Performance in Loops)
```python
parts = []
for i in range(5):
    parts.append(str(i))
result = ",".join(parts)
print(result)  # 0,1,2,3,4
```
> Interview-Recommended Pattern for large string building.

### 4G. Using * operator (for repetition)
```python
print("Na" * 4 + " Batman!")  # NaNaNaNa Batman!
```

## 5. Repetition
```python
print("Ha" * 3)   # HaHaHa
```
## 6. Membership Test
```python
s = "DevOps"
print("e" in s)    # True
print("x" not in s)  # True
```
## 7. Looping Through a String
```python
for char in "Code":
  print(char)
```
## 8. String Comparison
Lexicographical comparison (like dictionary order).
```python
print("apple" < "banana")   # True
print("Zoo" > "apple")      # False
```

## 9. `count(sub)`
```python
s = "banana"
print(s.count("a"))   # 3
```

## 10. String Reversal
```python
s = "Python"
print(s[::-1])   # nohtyP
```

## 11. Remove Characters
Remove vowels from a string:
```python
s = "apple"
result = ''.join([ch for ch in s if ch not in "aeiou"])
print(result)   # ppl
```
## 12. Check for Palindrome
```python
s = "madam"
print(s == s[::-1])   # True
```

## 13. Character Frequency Count
```python
from collections import Counter
s = "banana"
print(Counter(s))  # {'b': 1, 'a': 3, 'n': 2}
```

## 14. Remove Duplicates While Preserving Order
```python
s = "banana"
res = "".join(dict.fromkeys(s))
print(res)  # ban
```

## 15. ASCII Conversions
```python
print(ord('A'))  # 65
print(chr(65))   # A
```

---

# String Methods
# 1. Case Conversion Methods
| Method         | Description                           | Example                                   |
| -------------- | ------------------------------------- | ----------------------------------------- |
| `upper()`      | Converts all characters to uppercase  | `"hello".upper()` → `"HELLO"`             |
| `lower()`      | Converts all to lowercase             | `"HELLO".lower()` → `"hello"`             |
| `title()`      | Capitalizes first letter of each word | `"hello world".title()` → `"Hello World"` |
| `capitalize()` | Capitalizes only the first character of the string and converts the rest to lowercase | `"python IS awesOME".capitalize()` → `"Python is awesome"` |
| `swapcase()`   | Swaps uppercase ↔ lowercase           | `"PyThOn".swapcase()` → `"pYtHoN"`        |

# 2. Searching & Finding
| Method            | Description                                   | Example                              |
| ----------------- | --------------------------------------------- | ------------------------------------ |
| `find(sub)`       | Returns first index of `sub`, -1 if not found | `"banana".find("na")` → `2`          |
| `rfind(sub)`      | Returns last index of `sub`, -1 if not found  | `"banana".rfind("na")` → `4`         |
| `index(sub)`      | Like `find()`, but raises error if not found  | `"apple".index("p")` → `1`           |
| `rindex(sub)`     | Like `rfind()`, but raises error if not found | `"apple".rindex("p")` → `2`          |
| `startswith(sub)` | Returns True if string starts with `sub`      | `"python".startswith("py")` → `True` |
| `endswith(sub)`   | Returns True if string ends with `sub`        | `"test.py".endswith(".py")` → `True` |

# 3. Modifying Content
| Method              | Description                        | Example                               |
| ------------------- | ---------------------------------- | ------------------------------------- |
| `replace(old, new)` | Replaces all occurrences           | `"aabb".replace("a", "z")` → `"zzbb"` |
| `strip()`           | Removes whitespace from both sides | `" hello ".strip()` → `"hello"`       |
| `lstrip()`          | Removes left-side spaces           | `"  hello".lstrip()` → `"hello"`      |
| `rstrip()`          | Removes right-side spaces          | `"hello  ".rstrip()` → `"hello"`      |

# 4. Splitting and Joining
| Method             | Description                   | Example                                    |
| ------------------ | ----------------------------- | ------------------------------------------ |
| `split(delim)`     | Splits into list              | `"a,b,c".split(",")` → `['a','b','c']`     |
| `rsplit(delim)`    | Splits from right             | `"a,b,c".rsplit(",", 1)` → `['a,b', 'c']`  |
| `splitlines()`     | Splits on `\n` or line breaks | `"a\nb\nc".splitlines()` → `['a','b','c']` |
| `'sep'.join(list)` | Joins list into string        | `",".join(["a", "b"])` → `"a,b"`           |

# 5. Character Type Checking
| Method      | Description      | Example                            |
| ----------- | ---------------- | ---------------------------------- |
| `isalpha()` | Letters only     | `"abc".isalpha()` → `True`         |
| `isdigit()` | Digits only      | `"123".isdigit()` → `True`         |
| `isalnum()` | Letters + digits | `"abc123".isalnum()` → `True`      |
| `isupper()` | All uppercase    | `"ABC".isupper()` → `True`         |
| `islower()` | All lowercase    | `"abc".islower()` → `True`         |
| `isspace()` | Only whitespace  | `"  ".isspace()` → `True`          |
| `istitle()` | Title case       | `"Hello World".istitle()` → `True` |

# 6. Padding and Alignment
| Method                | Description     | Example                              |
| --------------------- | --------------- | ------------------------------------ |
| `center(width, fill)` | Centers string  | `"cat".center(7, "-")` → `"--cat--"` |
| `ljust(width, fill)`  | Left aligns     | `"cat".ljust(6, "*")` → `"cat***"`   |
| `rjust(width, fill)`  | Right aligns    | `"cat".rjust(6, "*")` → `"***cat"`   |
| `zfill(width)`        | Pads with zeros | `"42".zfill(5)` → `"00042"`          |


# 7. Encoding & Decoding
| Method     | Description              | Example                         |
| ---------- | ------------------------ | ------------------------------- |
| `encode()` | Converts string to bytes | `"hello".encode()` → `b'hello'` |
| `decode()` | Converts bytes to string | `b'hello'.decode()` → `"hello"` |

# 8. Other Utility Methods
| Method                        | Description                                  | Example                                  |
| ----------------------------- | -------------------------------------------- | ---------------------------------------- |
| `count(sub)`                  | Counts how many times `sub` occurs           | `"banana".count("a")` → `3`              |
| `format()`                    | String formatting (before f-strings)         | `"{} is {}".format("Python", "awesome")` |
| `casefold()`                  | Lowercase + more aggressive Unicode lowering | `"ß".casefold()` → `"ss"`                |
| `maketrans()` + `translate()` | Replace multiple characters                  | see below                                |




