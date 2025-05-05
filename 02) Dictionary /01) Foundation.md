
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

# Dictionary Operations 
## 1. Create / Initialize Dictionary
```python
d = {}  # Empty
d = dict()  # Also empty
d = {"a": 1, "b": 2}  # Predefined
```
**Use-case:**  
Variable to value mapping  
Frequency map 

## 2. Accessing Elements
#### i) `dict[key]` → Basic access using key 
ही सर्वात basic आणि fast method आहे (Time complexity: O(1))
```python
student = {'name': 'Sita', 'age': 22}
print(student['name'])  # Output: Sita
```
जर key exist नसेल तर KeyError येतो:
```python
print(student['city'])  # KeyError: 'city'
```
### ii) `dict.get(key, default=None)` → Safe access
```python
print(student.get('city'))            # Output: None
print(student.get('city', 'Unknown')) # Output: Unknown
```
जेव्हा तुम्हाला माहित नाही की key आहे की नाही, तेव्हा get() वापरावे.

```python
d = {"a": 10, "b": 20}
print(d["a"])         # 10
print(d.get("c", 0))  # 0 (safe fallback)
```
> `d["c"]` वापरल्यास → `KeyError` येईल.

### iii) `.keys()` → All keys access
Useful when only keys हव्यात आणि values नाही.
```python
print(student.keys())  # dict_keys(['name', 'age'])
```
Best Tip: `list(student.keys())` केल्यास index-based access करता येते.
```python
print(list(student.keys()))  # ['name', 'age']
```

### iv) `.values()` → All values access  
Useful when only values हव्यात आणि keys नाही.
```python
print(student.values())  # dict_values(['Sita', 22])
```
Best Tip: `list(student.values())` केल्यास index-based access करता येते.
```python
print(list(student.values()))  # ['Sita', 22]
```
### v) `.items()` → Access key-value pair एकत्र
Interview आणि CP मध्ये हे format जास्त वापरतात.
```python
for key, value in student.items():
    print(f"{key}: {value}")
```

## 3. Dictionary Searching / Checking

| Search Type                | काय शोधतो?                 | कसा वापरतो?                    |
| -------------------------- | -------------------------- | ------------------------------ |
| 🔑 Key exists check        | Key dictionary मधे आहे का? | `if key in dict`               |
| 🔍 Value exists check      | Value आहे का?              | `if value in dict.values()`    |
| 🧾 Key + Value check combo | Key आणि त्याचा value       | Loop वापरून (filter logic)     |
| 🔁 Condition-based search  | Complex filtering          | Loop + if/else + comprehension |

### i) `if key in dict` – Check if key exists
Dictionary मध्ये एखादा key आहे का ते शोधतो.
```python
student = {'name': 'Sita', 'age': 22}

if 'name' in student: print("Yes, key 'name' exists!")
else: print("Not found!")  # Yes, key 'name' exists!
```
Time complexity: O(1) - fast lookup -  हे सर्वात fast and efficient आहे कारण dictionary internally hashing वापरतो.

### ii) `if value in dict.values()` – Check if value exists
Dictionary मधील values मध्ये काही specific value आहे का?
```python
student = {'name': 'Sita', 'age': 22}

if 22 in student.values():
    print("Value 22 exists!")  # Value 22 exists!
```
dict.values() हे list-like object आहे, त्यामुळे मोठ्या dictionary मध्ये हे थोडं slow असू शकतं.  

### iii) Check key + value pair combo (manual search)
एखादा specific key + त्याचा specific value दोघेही आहेत का, हे पाहणं.
```python
student = {'name': 'Sita', 'age': 22}

if student.get('age') == 22:
    print("Key 'age' with value 22 exists")
```
Alternative: Loop वापरून
```python
for key, value in student.items():
    if key == 'age' and value == 22:
        print("Match found")
```

### iv) Multiple key check – using set logic
एखादा specific key + त्याचा specific value दोघेही आहेत का, हे पाहणं.
```python
student = {'name': 'Sita', 'age': 22, 'city': 'Pune'}

# Check if all keys exist
if {'name', 'age'}.issubset(student.keys()):
    print("Both keys exist")
```

### v) Filter all items with condition
Example: Find all students above age 20
```python
students = {
    'Amit': 21,
    'Sita': 19,
    'Raj': 23
}

# Dictionary comprehension
above_20 = {k: v for k, v in students.items() if v > 20}

print(above_20)  # {'Amit': 21, 'Raj': 23}
```

### vi) Search using `.get()` with default fallback
```python
student = {'name': 'Sita'}

age = student.get('age', 'Not Found')

print(age)  # Not Found
```

### vii) Count value frequency using `collections.Counter`
```python
from collections import Counter

votes = ['A', 'B', 'A', 'C', 'A', 'B']

count = Counter(votes)

print(count['A'])  # Output: 3
```
Useful for frequency counting in dictionaries.

## 4. `dict.setdefault(key, default)` → Access + Add if not exists
एकाच वेळी check + insert करण्यासाठी उपयोगी.
```python
user = {'id': 1}
name = user.setdefault('name', 'Unknown')
print(name)        # Output: Unknown
print(user)        # {'id': 1, 'name': 'Unknown'}
```

## 5. Add / Update Key-Value Pair
### i) `dict[key] = value`
> जर key असलीच तर update होतो.  
> जर key नसेल तर नवा key-value pair add होतो.

```python
d["new_key"] = new_value  # Add
d["existing_key"] = new_value  # Update
```
```python
student = {'name': 'Sita', 'age': 22}
# ✅ Update existing key
student['age'] = 23

# ✅ Add new key-value
student['city'] = 'Pune'  

print(student)  # {'name': 'Sita', 'age': 23, 'city': 'Pune'}
```
### ii) Using `dict.update()` method  
एकाच वेळी एक किंवा अनेक key-value pairs add/update करू शकतो.
```python
# syntax
dict.update({key: value})
```
```python
student = {'name': 'Sita'}

# ✅ Add multiple keys
student.update({'age': 22, 'city': 'Mumbai'})

# ✅ Update existing key
student.update({'city': 'Nagpur'})

print(student)  # {'name': 'Sita', 'age': 22, 'city': 'Nagpur'}
```

### iii) Using Dictionary Unpacking (**) – Python 3.5+
दोन dictionaries merge करून नवीन dictionary तयार करतो.  
> Note: ह्यामुळे नवीन dictionary तयार होते (immutable update).

```python
student = {'name': 'Sita'}
new_data = {'age': 22, 'city': 'Pune'}

# ✅ Merge two dicts using unpacking
student = {**student, **new_data}

print(student)  # {'name': 'Sita', 'age': 22, 'city': 'Pune'}
```

### iv) Using `setdefault()`
जर key नसेल, तर add होतो with default value.  
जर key already असेल, काहीही update होत नाही.  
```python
student = {'name': 'Sita'}

# Add if not exists
student.setdefault('age', 22)

# No change since 'name' already exists
student.setdefault('name', 'Radha')

print(student)  # {'name': 'Sita', 'age': 22}
```

## 6. Delete Elements
### i) `del dict[key]` – Specific key-value pair delete करतो
Mhanje `Dict` मधून एखादा key-value pair delete करतो.  

```python
student = {'name': 'Sita', 'age': 22}

# Delete the 'age' key
del student['age']

print(student)  #  {'name': 'Sita'}
```
⚠️ जर key नसेल तर KeyError येतो! 
> Handle with check: 
```python
if 'age' in student:
    del student['age']
```
### ii) `.pop(key, default)` – Delete + Return
Delete करतो आणि त्याच key चा value return करतो.

```python
student = {'name': 'Sita', 'age': 22}

age_value = student.pop('age')

print(age_value)  # 22
print(student)    # {'name': 'Sita'}
```
⚠️ जर key नसेल तर KeyError येतो. Optional default वापरून handle करू शकतो.
```python
student = {'name': 'Sita'}
value = student.pop('age', 'Not Found')
print(value)  # Not Found
```
### iii) `.popitem()` – Last inserted item काढतो (Python 3.7+)
Last added key-value pair काढतो आणि tuple स्वरूपात return करतो.

```python
student = {'name': 'Sita', 'age': 22, 'city': 'Pune'}

item = student.popitem()

print(item)       # ('city', 'Pune')
print(student)    # {'name': 'Sita', 'age': 22}
```
⚠️ जर dictionary खाली (empty) असेल तर KeyError येतो.

### iv) `.clear()` – सगळी key-value pairs delete
Dictionary पूर्णपणे साफ करतो (empty करतो).
```python
student = {'name': 'Sita', 'age': 22}

student.clear()

print(student)  # {}
```

### v) `del dict` – Complete dictionary object delete
संपूर्ण dictionary object delete होतो.
```python
student = {'name': 'Sita'}

del student

# print(student)  # ❌ Error: NameError – student is not defined
```

### Summary
| Method           | Purpose                              | Deletes Key? | Returns Value? |
| ---------------- | ------------------------------------ | ------------ | -------------- |
| `del dict[key]`  | Delete specific key                  | ✅            | ❌              |
| `dict.pop(key)`  | Delete specific key and return value | ✅            | ✅              |
| `dict.popitem()` | Remove **last inserted** item        | ✅            | ✅ (tuple)      |
| `dict.clear()`   | Remove all items                     | ✅ (all)      | ❌              |
| `del dict`       | Delete entire dictionary object      | ✅ (object)   | ❌              |

## 7. Length of list
```python
print(len(mylist))  # 3
```
`len()` on dictionary is O(1) — fast because Python internally tracks size.

## 8. Slicing
Dictionary ला direct slicing करता येत नाही (like list/string).  
This is not Valid:
```python
my_dict = {'a': 1, 'b': 2, 'c': 3}
# print(my_dict[0:2])  ❌ This gives: TypeError
```
Dictionary मध्ये indexing नसते (unordered structure – until Python 3.7+ retains insertion order, but not indexable like lists).  
### तरीही, आपल्याला “सारखं” काम हवं असेल, तर पुढील techniques वापरता येतात:  
### i)  Dictionary to List Conversion and then Slicing  
Eg. : dictionary मधील first n elements घ्यायचे असतील.  
```python
my_dict = {'a': 1, 'b': 2, 'c': 3, 'd': 4}

# Convert to list of tuples, slice first 2 elements
sliced = dict(list(my_dict.items())[:2])

print(sliced)  # {'a': 1, 'b': 2}
```

### ii) Slicing Only Keys  
```python
my_dict = {'a': 1, 'b': 2, 'c': 3, 'd': 4}

keys = list(my_dict.keys())[1:3]  # Slice index 1 to 2 → ['b', 'c']

print(keys)
```
जर full sliced dictionary पाहिजे असेल:
```pythion
sliced = {k: my_dict[k] for k in list(my_dict.keys())[1:3]}

print(sliced)  # {'b': 2, 'c': 3}
```

### iii) Slicing by Condition (Filter Style)
Eg. : सगळी values > 10 असलेली pairs retain करायची
```python
prices = {'apple': 10, 'banana': 5, 'cherry': 15, 'grapes': 8}

sliced = {k: v for k, v in prices.items() if v > 10}

print(sliced)  # {'cherry': 15}
```
CP मध्ये conditional slicing फार उपयोगी padte

## 9. Loop Through Dictionary
### i) Loop through keys 
By default, for key in dict हे keys वरच iterate करतं.
```python
student = {'name': 'Rahul', 'age': 21, 'grade': 'A'}

for key in student:
    print(key)
```
output:
```python
name
age
grade
```

### ii) Loop through values
```python
for value in student.values():
    print(value)
```
output:
```python
Rahul
21
A
```

### iii) Loop through key-value pairs
```python
for key, value in student.items():
    print(f"{key} => {value}")
```
output:
```python
name => Rahul
age => 21
grade => A
```


### iv) Loop through sorted keys
```python
for key in sorted(student):
    print(f"{key} => {student[key]}")
```
output:
```python
age => 21
grade => A
name => Rahul
```
`sorted()` वापरल्याने keys alphabetically sort होतात.  

### v) Loop through keys with `enumerate()` (indexing)
```python
for idx, key in enumerate(student):
    print(f"{idx}: {key} => {student[key]}")
```
output:
```python
0: name => Rahul
1: age => 21
2: grade => A
```
`enumerate()` वापरल्याने तुम्हाला index number पण मिळतो.

### vi) Reverse Loop
```python
for key in reversed(list(student)):
    print(f"{key} => {student[key]}")
```
output:
```python
grade => A
age => 21
name => Rahul
```
Reversed order मध्ये loop करायचा असल्यास `reversed()` वापरतो.

### vii) Loop over Nested Dictionary
```python
students = {
    'Rahul': {'age': 21, 'grade': 'A'},
    'Neha': {'age': 22, 'grade': 'B'}
}

for name, info in students.items():
    print(f"{name}'s Info:")
    for key, value in info.items():
        print(f"  {key} => {value}")
```
output:
```python
Rahul's Info:
  age => 21
  grade => A
Neha's Info:
  age => 22
  grade => B
```
हे interviews साठी खूप महत्त्वाचं pattern आहे — nested dict वर loop टाकणे.

### Bonus: Dictionary Comprehension with Loop
```python
squares = {x: x*x for x in range(1, 6)}
print(squares)  # {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
```
Dictionary comprehension = loop + conditional logic → neat and concise dict creation

## 10. Sort a Dictionary
Dictionary म्हणजे unordered collection (Python 3.6+ पासून insertion order preserve होतो, पण sort नाही).  
Sorting करायचं असेल तर sorted() वापरावं लागतं — पण dict वर directly sort लावता येत नाही, त्याचे keys, values किंवा items sort करून नवीन dict तयार करावी लागते.

### i) Sort by Keys (Ascending)
```python
student = {'name': 'Rahul', 'age': 21, 'grade': 'A'}

sorted_by_keys = dict(sorted(student.items()))
print(sorted_by_keys)
```
output:
```python
{'age': 21, 'grade': 'A', 'name': 'Rahul'}
```
`sorted(student.items())` हे list of tuples return करतं, जे dictionary च्या key-value pairs असतात आणि हे sort केलेले असतात keys वर ascending order मध्ये.  
`sorted(dict.items())` हे key वर sort करतं कारण items हे (key, value) pair असतात.  

### ii) Sort by Keys (Descending)
```python
sorted_by_keys_desc = dict(sorted(student.items(), reverse=True))
print(sorted_by_keys_desc)
```
output:
```python
{'name': 'Rahul', 'grade': 'A', 'age': 21}
```

### iii) Sort by Values (Ascending)
```python
sorted_by_values = dict(sorted(student.items(), key=lambda item: item[1]))
print(sorted_by_values)
```
output:
```python
{'grade': 'A', 'name': 'Rahul', 'age': 21}
```
`item[1]` म्हणजे value वर sort

### iv) Sort by Values (Descending)
```python
sorted_by_values_desc = dict(sorted(student.items(), key=lambda item: item[1], reverse=True))
print(sorted_by_values_desc)
```
output:
```python
{'age': 21, 'name': 'Rahul', 'grade': 'A'}
```

## 11. Reverse a Dictionary
Dictionary ला direct reverse करता येत नाही, पण keys किंवा items चा order उलटा करून करता येतं.  

### i) Reverse Insertion Order
```python
student = {'name': 'Rahul', 'age': 21, 'grade': 'A'}
reversed_dict = dict(reversed(list(student.items())))
print(reversed_dict)
```
output:
```python
{'grade': 'A', 'age': 21, 'name': 'Rahul'}
```
### ii) Reverse Keys List
```python
for key in reversed(student):
    print(f"{key} => {student[key]}")
```
output:
```python
grade => A
age => 21
name => Rahul
```
### iii) Reverse using Dictionary Comprehension
```python
rev_dict = {k: student[k] for k in reversed(student)}
print(rev_dict)
```
output:
```python
{'grade': 'A', 'age': 21, 'name': 'Rahul'}
```


## 12. Joining Dictionaries (Dict Merge)
### i) Using `update()`
```python
dict1 = {'a': 1, 'b': 2}
dict2 = {'b': 3, 'c': 4}

dict1.update(dict2)
print(dict1)   # {'a': 1, 'b': 3, 'c': 4}

```
> Note: Common key ('b') ची value dict2 ने overwrite केली.

### ii) Using `|` (Python 3.9+)
```python
dict1 = {'a': 1, 'b': 2}
dict2 = {'c': 3}

merged = dict1 | dict2
print(merged)  # {'a': 1, 'b': 2, 'c': 3}
```
> Note: | operator एक नवीन dictionary return करतो – original dicts modify होत नाहीत.  

### iii) Using dictionary unpacking (**)
```python
dict1 = {'a': 1}
dict2 = {'b': 2}
merged = {**dict1, **dict2}
print(merged)  # {'a': 1, 'b': 2}
```

## 13. Conversion Operations
### i) Convert List of Tuples → Dictionary
```python
pairs = [('a', 1), ('b', 2)]
d = dict(pairs)
print(d)   # {'a': 1, 'b': 2}
```

### ii) Convert Two Lists → Dictionary using `zip()`
```python
keys = ['a', 'b', 'c']
values = [1, 2, 3]

d = dict(zip(keys, values))
print(d)  # {'a': 1, 'b': 2, 'c': 3}
```

### iii) Convert Dictionary → List of Keys, Values, or Items
```python
d = {'a': 1, 'b': 2}

print(list(d.keys()))    # ['a', 'b']
print(list(d.values()))  # [1, 2]
print(list(d.items()))   # [('a', 1), ('b', 2)]
```
### iv) Convert Dictionary → String
```python
d = {'a': 1, 'b': 2}
s = str(d)
print(s)   # "{'a': 1, 'b': 2}"
```
### v) Convert String → Dictionary using `json.loads()`
```python
import json

s = '{"a": 1, "b": 2}'
d = json.loads(s)
print(d)  # {'a': 1, 'b': 2}
```

### vi) Convert Dictionary → JSON string using `json.dumps()`
```python
import json

d = {'a': 1, 'b': 2}
s = json.dumps(d)
print(s)  # '{"a": 1, "b": 2}'
```

## 14. Miscellaneous
### i) `copy()` – Clone Dictionary (Shallow Copy)
```python
original = {'a': 1, 'b': 2}
copy_dict = original.copy()
print(copy_dict)  # {'a': 1, 'b': 2}
```
Note: हा shallow copy असतो – nested structures असेल तर ते shared असतात.  

### ii) `fromkeys()` – List मधून key तयार करणे
```python
keys = ['name', 'age', 'gender']
default_value = None
d = dict.fromkeys(keys, default_value)
print(d)  # {'name': None, 'age': None, 'gender': None}
```

### iii) `setdefault()` – Default value assign करतो (जर key नसेल तर)
```python
student = {'name': 'Ravi'}
student.setdefault('age', 25)
student.setdefault('name', 'Akash')  # already exists

print(student)  # {'name': 'Ravi', 'age': 25}
```

### iv) Dictionary Equality Check – Compare two dictionaries
```python
d1 = {'a': 1, 'b': 2}
d2 = {'b': 2, 'a': 1}
print(d1 == d2)  # True
```
Key order important नाही Python dict मध्ये (>=3.7 retains order, but equality doesn't care about it)

## Aggregate Functions
Example Dictionary: 
```python
scores = {
    'Ravi': 88,
    'Sneha': 92,
    'Amit': 76,
    'Neha': 85
}
```

### 1. `sum()` – सगळ्या values ची बेरीज
```python
total = sum(scores.values())
print(total)  # Output: 88 + 92 + 76 + 85 = 341
```

### 2. `max()` – सर्वात जास्त score (value) किंवा नाव (key)
```python
max_score = max(scores.values())  # By value
print(max_score)  # 92

topper = max(scores, key=scores.get)  # कोणाचा आहे?
print(topper)  # Sneha
```

### 3. `min()` – सगळ्यात कमी score
```python
min_score = min(scores.values())  # 76
weakest = min(scores, key=scores.get)
print(weakest)  # Amit
```

### 4. `sorted()` – Ordered view by values
```python
count = len(scores)
print(count)  # Output: 4
```
### 5. Top N scorers (advanced)
```python
top_2 = sorted(scores.items(), key=lambda item: item[1], reverse=True)[:2]
print(top_2)
# [('Sneha', 92), ('Ravi', 88)]
```
### 6. statistics.mean() – Average काढण्यासाठी (Python inbuilt lib)
```python
# Ascending order of scores
sorted_by_value = sorted(scores.items(), key=lambda item: item[1])
print(sorted_by_value)
# [('Amit', 76), ('Neha', 85), ('Ravi', 88), ('Sneha', 92)]
```
### 7. `len()` – किती entries आहेत (keys count)
```python
count = len(scores)
print(count)  # Output: 4
```

