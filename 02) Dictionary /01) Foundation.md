
# Pythonic-Brain
## Dictionary 
Python dictionary हा एक key-value pair based data structure आहे. म्हणजे प्रत्येक element एक "key" आणि त्याचा "value" याचा एक जोड (pair) असतो.  
**Structure:**  
```python
my_dict = {
    "name": "Ajay",
    "age": 25,
    "is_student": True
}
```
इथे `"name"`, `"age"`, `"is_student"` हे `keys` आहेत आणि `"Ajay"`, `25`, `True` हे त्यांचे `values` आहेत.  

## Characteristics 
| विशेषता (Feature)        | स्पष्टीकरण (Explanation)                                                                        |
| ------------------------ | ----------------------------------------------------------------------------------------------- |
| 🔑 Keys unique असतात     | dictionary मधे प्रत्येक key फक्त एकदाच असतो. जर duplicate key असेल, तर शेवटचा value ठेवला जातो. |
| ⏩ Order preserved (3.7+) | Python 3.7 पासून dictionaries *insertion order* maintain करतात.                                 |
| ⚡ Fast access            | तुम्हाला key दिल्यावर value पटकन मिळतो — *O(1) time complexity*.                                |
| 🔄 Mutable               | dict मध्ये values तुम्ही update करू शकता (changeable).                                          |
| 🔒 Immutable key only    | keys म्हणून फक्त immutable data types (जसे की string, number, tuple) चालतात.                    |


### 1. Key-Value Pair Data Structure  
Dictionary ही एक mapping data structure आहे जिथे key unique असतो आणि त्याच्या corresponding value स्टोअर केली जाते.
```python
student = {"name": "Ravi", "age": 21, "branch": "CS"}
```
> `"name"` ही `key` आहे आणि `"Ravi"` ही त्याची `value`.  
> आपल्याला हवं तेवढं information एका ठिकाणी एकदम structured पद्धतीने ठेवता येतं.
> Access: `student["branch"]` → `"CS"`

**Use-case in CP:** 
Mapping of elements → frequency, ID-to-data mapping, etc.  
Example: Count frequency of elements.  
```python
arr = [1, 2, 2, 3, 1, 4]
freq = {}
for num in arr:
    freq[num] = freq.get(num, 0) + 1
print(freq)
# Output: {1: 2, 2: 2, 3: 1, 4: 1}
```
### 2. Keys must be Immutable
Dictionary keys हे hashable असायला हवेत, म्हणजेच immutable types (str, int, tuple) असायला हवेत.  
`str`, `int`, `float`, `bool`, `tuple` ✅  
❌ `list`, `dict`, `set` → हे चालत नाहीत → कारण त्यांचे value बदलता येतात (mutable → unhashable)

Valid Example:
```python
d = {(1, 2): "point", "name": "Sam"}
```
Invalid Example:
```python
d = {(1, 2): "point", "name": "Sam"}
```
आपल्याला composite key वापरायची असेल (e.g., (x, y) coordinates), तर tuple best आहे.  
Interviewers अक्सर "can list be a dictionary key?" असं विचारतात.  
**Use-case in CP:** Coordinates-based keys वापरायला (x, y) ⇒ `dict[(x, y)] = value`  

### 3. Keys are Unique
Dictionary मध्ये प्रत्येक `key` unique असतो. Duplicate key दिल्यास नवीन `value` जुन्यावर overwrite होते.  
```python
d = {"a": 1, "b": 2, "a": 3}
print(d)  # Output: {'a': 3, 'b': 2}
```
> "a" key दुसऱ्यांदा assign झालं, त्यामुळे tyachi value 1 नाही तर 3 राहिलं.  
> Key always unique असतो, values duplicate चालतात.  
> Hash-based mapping problems (like frequency counts) मध्ये ही uniqueness वापरतो.    
> For example, counting characters, words, or elements using frequency map.

### 4. Lookup Time Complexity is O(1)  
Dictionary internally hash table वर आधारित असतो. त्यामुळे dict[key] ही operation सरासरीत O(1) वेळ घेते.  

```python
d = {"x": 10, "y": 20}
print(d["x"])  # O(1) → 10
```
**Use-case in CP:**  
Large inputs असलेल्या problems मध्ये dictionary चा वापर करून brute force O(n²) → O(n) करू शकतो.  
HashMap-based optimizations are very common in Leetcode, CP.  
```python
# Two sum problem
nums = [2, 7, 11, 15]
target = 9
d = {}
for i, num in enumerate(nums):
    if target - num in d:
        print([d[target - num], i])
    d[num] = i
```

### 5. Ordered Since Python 3.7+  
Python 3.7 पासून, dictionary retains insertion order.  
Previously (before 3.7), dictionary order was random.  
आता जो order ने तुम्ही insert करता, तोच print/order मध्ये राहतो.  
```python
d = {"one": 1, "two": 2, "three": 3}
print(d)  # {'one': 1, 'two': 2, 'three': 3}
```
**Use-case in CP:** Order-sensitive output required? → dict वापरू शकतो safely.  
Interviewers काही वेळा असा trick प्रश्न विचारतात: "Will dict maintain the order?"

### 6. Mutable Structure
Dictionary ही mutable आहे — आपण त्यात elements add, update, delete करू शकतो.  
Flexibility मिळते – dynamic input, state store करण्यासाठी.  
```python
d = {}
d["a"] = 1        # Add
d["a"] = 5        # Update
del d["a"]        # Delete
print(d)          # Output: {}
```
**Use-case in CP:** Memoization in recursion
```python
dp = {}
def fib(n):
    if n <= 1:
        return n
    if n in dp:
        return dp[n]
    dp[n] = fib(n-1) + fib(n-2)
    return dp[n]
```
### 7. Supports Nested Dictionaries
Dictionary च्या value म्हणून अजून एक dictionary ठेवता येतो.  
Complex data structures manage करायला मदत होते.

```python
emp = {
    "emp1": {"name": "Ravi", "age": 30},
    "emp2": {"name": "Neha", "age": 28}
}
print(emp["emp1"]["name"])  # Ravi
```
**Use-case in CP:** Tree, Trie, Graph representation.

### 8. Dynamic Size
Dictionary dynamically grow होतो. आपण key-value pair add करत जाऊ शकतो.   
No need to declare size like arrays/lists.  
On-the-fly input management possible.  

```python
d = {}
for i in range(5):
    d[i] = i*i
print(d)  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

### 9. Safe Lookup Using `.get()`
`.get(key, default)` वापरल्यास जर key नसेल तर error न देता default return करतो.

```python
d = {"x": 10}
print(d.get("y", 0))  # Output: 0 (safe fallback)
```
> `d["y"]` वापरल्यास KeyError आला असता.  
> `.get()` वापरल्यामुळे program crash होत नाही.

**Use-case in CP:** Safe counting, missing value access
```python
freq = {}
for ch in "aabbc":
    freq[ch] = freq.get(ch, 0) + 1
```
###  10. Powerful Built-in Methods
| Method              | Example                 | Explain                        |
| ------------------- | ----------------------- | ------------------------------ |
| `d.items()`         | `for k,v in d.items():` | Iterate over key-value         |
| `d.keys()`          | `for k in d.keys():`    | All keys                       |
| `d.values()`        | `for v in d.values():`  | All values                     |
| `d.update({k:v})`   | `d.update({"a": 5})`    | Add/overwrite                  |
| `d.pop("a")`        | `d.pop("a")`            | Delete key & return value      |
| `d.setdefault(k,v)` | `d.setdefault("x", 10)` | Add default if key not present |
| `d.clear()`         | `d.clear()`             | Remove all elements            |

## Dictionary Operations 
### 1. Create / Initialize Dictionary
```python
d = {}  # Empty
d = dict()  # Also empty
d = {"a": 1, "b": 2}  # Predefined
```
**Use-case:**  
Variable to value mapping  
Frequency map  
### 2. Accessing Elements
```python
d["a"]  # Direct access
d.get("b", default_value)  # Safe access
```
```python
d = {"a": 10, "b": 20}
print(d["a"])         # 10
print(d.get("c", 0))  # 0 (safe fallback)
```
> `d["c"]` वापरल्यास → `KeyError` येईल.

### 3. Key Exists का तपासणे - `in` Operator
```python
if 'age' in person:
    print("Age is present")
```
Time complexity: O(1) - fast lookup

### 4. Add / Update Key-Value Pair
```python
d["new_key"] = new_value  # Add
d["existing_key"] = new_value  # Update
```
```python
d = {}
d["x"] = 5  # Add
d["x"] = 10  # Update
print(d)  # {'x': 10}
```
### 4. Delete a key-value pair
**`del dict[key]` → Delete a key-value pair**  
जर key नसेल, तर `KeyError`.
```python
del person['city']
```
**`.pop(key, default)` → Remove & Return Value**  
Safe delete with return.  
```python
age = person.pop('age', None)
print(age)  # Output: 30
```
**`.popitem()` → Remove & return last inserted item**
```python
mylist.extend([60, 70])
print(mylist)  # [10, 50, 99, 30, 40, 60, 70]
```

##################
### 5. Delete Elements
**`pop()` – Remove last**  
```python
mylist.pop()  # removes 70
print(mylist)
```
**`pop(index)` – Remove specific index**  
```python
mylist.pop(1)  # removes 50
print(mylist)
```
**`remove(value)` – Remove by value**  
```python
mylist.remove(99)
print(mylist)
```
**`clear()` – Remove all elements**  
```python
mylist.clear()
print(mylist)  # []
```
### 6. Search/Check Elements
**`in` keyword**  
```python
mylist = [1, 2, 3]
print(2 in mylist)   # True
print(5 in mylist)   # False
```
**`index()` – Find position**  
`index(x, start_index, end_index)` asa asto main mhanje pn tyalae `start_index` ani `end_index` optional astat
```python
print(mylist.index(2))  # 1

lst = [10, 20, 30, 20]
print(lst.index(20))       # 1
print(lst.index(20, 2))    # 3
```
**`count()` – How many times value appears**  
```python
print(mylist.count(3))  # 1
```
### 7. Length of list
```python
print(len(mylist))  # 3
```
### 8. Slicing
**Basic**  
```python
nums = [10, 20, 30, 40, 50]
print(nums[1:4])    # [20, 30, 40]
```
**Step slicing**  
```python
print(nums[::2])    # [10, 30, 50]
```
**Reverse slicing**  
```python
print(nums[::-1])   # [50, 40, 30, 20, 10]
```
### 9. Loop through List
**Using for loop**  
```python
for x in nums:
    print(x)
```
**Using while loop**  
```python
i = 0
while i < len(nums):
    print(nums[i])
    i += 1
```
**With enumerate() – gives index and value**  
```python
for idx, val in enumerate(nums):
    print(f"Index {idx}, Value {val}")
```
> Note: fakt list sobat ch nhi tr enumerate baki data structures sobat pn use karu shakato  
> eg. in case of hashmap -> `for inx, (key, val) in enumerate(hashmap)` asa yeyil

### 10. Sort & Reverse
**`sort()` – in-place**  
`sort(key=None, reverse=False)` asa asto main function. but Optional: `reverse=True`, `key=custom_function`.
> both `sort()` ani `sorted()` internally TimSort use kartat -  `TimSort = Merge Sort + Insertion Sort hybrid`
```python
nums.sort()
print(nums)

lst = [3, 1, 2]
lst.sort()
print(lst)  # [1, 2, 3]

lst.sort(reverse=True)
print(lst)  # [3, 2, 1]
```
**`sorted()` – creates new list**  
```python
print(sorted(nums))  # sorted in ascending
print(sorted(nums, reverse=True))  # sorted in descending
```
**`reverse()` – just reverses order**  
```python
nums.reverse()
print(nums)
```
### 11. Copying a list
**Shallow copy**  
```python
copy1 = nums.copy()
```
**Slicing method**  
```python
copy2 = nums[:]
```

### 12. Join/Convert
**List to String**  
```python
chars = ['a', 'b', 'c']
print(''.join(chars))  # "abc"
```
**String to List**  
```python
s = "hello"
print(list(s))  # ['h', 'e', 'l', 'l', 'o']
```
### 13. List Comprehension
**Basic**  
```python
squares = [x*x for x in range(5)]
print(squares)  # [0, 1, 4, 9, 16]
```
**With condition**  
```python
evens = [x for x in range(10) if x % 2 == 0]
print(evens)  # [0, 2, 4, 6, 8]
```
### 14. Nested Lists (2D Lists)
**`reverse()` – just reverses order**  
```python
matrix = [
  [1, 2],
  [3, 4],
  [5, 6]
]
print(matrix[1][1])  # 4

# Loop through matrix
for row in matrix:
    for val in row:
        print(val)
```
### 15. Miscellaneous
**`max()`, `min()`, `sum()`**
```python
print(max(nums))  # Max value
print(min(nums))  # Min value
print(sum(nums))  # Sum
```
