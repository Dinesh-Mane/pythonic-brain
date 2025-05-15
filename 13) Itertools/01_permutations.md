# `itertools.permutations()`
`itertools.permutations()` is a function that returns all possible orderings (permutations) of a given iterable  
> Permutation: An ordered arrangement of elements.  
> For example: permutations of [1, 2] are → (1, 2) and (2, 1)

Syntax:
```python
from itertools import permutations

permutations(iterable, r=None)
```
- `iterable`: Any iterable (like list, string, tuple).
- `r`: Length of each permutation. If not specified, defaults to len(iterable).

**Returns:** An iterator that yields tuples, each being a permutation of length `r`.

# All Possible Scenarios:
| #  | Scenario                                        | Notes                                           |
| -- | ----------------------------------------------- | ----------------------------------------------- |
| 1  | Full-length permutations                        | `r=None` gives all orderings of entire iterable |
| 2  | Fixed-length permutations                       | `r=2`, `r=3`, etc.                              |
| 3  | Permutations of strings                         | `'abc'` → `abc, acb, ...`                       |
| 4  | Permutations with duplicate elements            | `set(permutations(...))` used for uniqueness    |
| 5  | Use in anagrams / string problems               | Anagram finder, scramble checker                |
| 6  | Use in backtracking-style generation            | Try every configuration                         |
| 7  | Lexicographic order generation                  | Sorted permutations list                        |
| 8  | Performance discussion                          | O(n!) complexity and iterator memory benefit    |
| 9  | Use in puzzles (tile/board)                     | All tile arrangements                           |
| 10 | Use with numbers (e.g. lock combinations)       | Brute-force style cracking                      |
| 11 | Manual dry-run explained                        | With 2 elements for clarity                     |
| 12 | Combined with `.join()` for strings             | `''.join(p)`                                    |
| 13 | Edge case with `r > len(iterable)`              | Should be covered                               |
| 14 | Empty iterable / edge case `[]`                 | Should be added                                 |
| 15 | Using in comparison with next permutation logic | Lexicographic applications                      |
| 16 | Convert iterator to list safely                 | `list(permutations(...))`                       |
| 17 | In-place usage with generators (not storing)    | `for p in permutations(...)`                    |
| 18 | Unique permutations in coding platforms         | Via `set()` or backtracking                     |

---

## 1. Full-Length Permutations (default r = len(iterable))
**Explanation:** When you call permutations(iterable) without specifying `r`, Python assumes `r = len(iterable)`. It generates all possible orderings using all elements.  
**Problem statement:** Generate all permutations of a given list using every element exactly once.  
```python
from itertools import permutations

data = [1, 2, 3]
for p in permutations(data):
    print(p)
```
Output:
```python
(1, 2, 3)
(1, 3, 2)
(2, 1, 3)
(2, 3, 1)
(3, 1, 2)
(3, 2, 1)
```
3 elements ⇒ 3! = 6 permutations


## 2. Fixed-Length Permutations (r specified)
**Explanation:** You can specify `r` to get permutations of only `r` elements at a time.   
**Problem statement:** Generate all permutations of length `r` from a given list.  
```python
from itertools import permutations

data = [1, 2, 3]
for p in permutations(data, 2):
    print(p)
```
Output:
```python
(1, 2)
(1, 3)
(2, 1)
(2, 3)
(3, 1)
(3, 2)
```
This gives P(3, 2) = 6 permutations


## 3. Permutations of Strings
**Explanation:** Strings are iterable, so each character is treated as an element. You can generate all character-level permutations.  
**Problem statement:** Find all rearrangements of characters in a string.    
```python
from itertools import permutations

word = "abc"
for p in permutations(word):
    print(''.join(p))
```
Output:
```python
abc
acb
bac
bca
cab
cba
```

## 4. Permutations with Duplicate Elements
**Explanation:** If the input contains duplicate elements, `permutations()` will return repeated tuples. To get only unique permutations, convert the result to a `set`  
**Problem statement:** Generate all unique permutations of a list that may contain duplicate elements.  
```python
from itertools import permutations

data = [1, 1, 2]
unique_perms = set(permutations(data))
for p in unique_perms:
    print(p)
```
Output:
```python
(1, 1, 2)
(1, 2, 1)
(2, 1, 1)
```


## 5. Use in Anagram or Scrambled String Problems
**Explanation:** By generating all permutations of a word, we can check if it matches known valid words in a dictionary – perfect for anagram detection or word scramble solving  
**Problem statement:** Find all valid anagram words from the permutations of a given word  
```python
from itertools import permutations

word = "tap"
dictionary = {"apt", "pat", "tap", "top", "pot", "opt"}

anagrams = set(''.join(p) for p in permutations(word))
valid_anagrams = anagrams & dictionary
print(valid_anagrams)
```
Output:
```python
{'apt', 'tap', 'pat'}
```


## 6. Use in Backtracking-Style Generation
**Explanation:** In recursive or backtracking problems (like Sudoku, N-Queens, etc.), we often try every possible configuration. permutations() helps us simulate all combinations without recursion when constraints are light.  
**Problem statement:** Generate all possible arrangements of 4 distinct digits to brute-force guess a passcode  
```python
from itertools import permutations

digits = [1, 2, 3, 4]
for attempt in permutations(digits):
    print(attempt)
```
Output:
```python
(1, 2, 3, 4)
(1, 2, 4, 3)
...
(4, 3, 2, 1)
```
Simulates full search space like recursive DFS/backtracking

## 7. Lexicographic Order Generation
**Explanation:**  `itertools.permutations()` generates results in lexicographic (dictionary) order if the input is sorted. This is useful when problems need permutations in increasing order.  
**Problem statement:** List all sorted permutations of the string 'bca' in lexicographic order.  
```python
from itertools import permutations

word = "bca"
for p in permutations(sorted(word)):
    print(''.join(p))
```
Output:
```python
abc
acb
bac
bca
cab
cba
```
Automatically sorted since input is sorted

## 8. Performance Discussion
**Explanation:**  
- Total permutations = n! (factorial)
- So time complexity = O(n!)
- But since permutations() returns an iterator, it doesn't store all in memory. You get items one by one, making it memory-efficient.

**Problem statement:** Iterate over permutations of a large list one-by-one without memory overload.  
```python
from itertools import permutations

big_data = list(range(10))  # 10! = 3628800 permutations

perm_gen = permutations(big_data)  # returns a generator

# Fetch only first 5 permutations
for _ in range(5):
    print(next(perm_gen))
```
Output:
```python
(0, 1, 2, 3, 4, 5, 6, 7, 8, 9)
(0, 1, 2, 3, 4, 5, 6, 7, 9, 8)
...
```
Efficiently handles huge spaces with low memory usage.

## 9. Use in Puzzles (Tile/Board)
**Explanation:** In board games or puzzles (e.g., 8-tile puzzle, Rubik’s cube flat representations), we often explore all tile arrangements to reach or validate a solution.  
**Problem statement:** Generate all possible tile arrangements for a 3-tile linear puzzle.  
```python
from itertools import permutations

tiles = ['red', 'blue', 'green']
for layout in permutations(tiles):
    print(layout)
```
Output:
```python
('red', 'blue', 'green')
('red', 'green', 'blue')
('blue', 'red', 'green')
('blue', 'green', 'red')
('green', 'red', 'blue')
('green', 'blue', 'red')
```
Useful in simulation, checking solvability, or search trees

## 10. Use with Numbers (e.g., Lock Combinations)
**Explanation:** When you want to brute-force a lock combination (4-digit pin, keypad pattern), use permutations of the digits.
**Problem statement:** Brute-force crack a 3-digit lock where digits are unique.
```python
from itertools import permutations

digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

for combo in permutations(digits, 3):
    print(combo)
```
Output:
```python
(0, 1, 2)
(0, 1, 3)
...
(9, 8, 7)
```
Perfect for simulating pin attacks, testing, or solving math puzzles

## 11. Manual Dry-Run Explained (with 2 elements)
**Explanation:** Understanding how permutations work with a small, simple example helps you reason through larger problems. Dry-runs are helpful during interviews.  
**Problem statement:** Manually simulate how permutations of two elements are generated  
```python
from itertools import permutations

data = [10, 20]
for p in permutations(data):
    print(p)
```
Output:
```python
(10, 20)
(20, 10)
```
Manual Dry Run:
```yaml
data = [10, 20]

Permutations of length 2:
- First position: 10 → Remaining: 20 → (10, 20)
- First position: 20 → Remaining: 10 → (20, 10)
```

## 12. Combined with `.join()` for Strings
**Explanation:** `itertools.permutations()` returns tuples, even for strings. Use `''.join(p)` to convert tuples into strings — especially useful for scrambled word solving, anagrams, etc.   
**Problem statement:** Generate all letter permutations of `'abc'` as full strings, not tuples.  
```python
from itertools import permutations

word = "abc"
for p in permutations(word):
    print(''.join(p))
```
Output:
```python
abc
acb
bac
bca
cab
cba
```



## 13. Edge Case with `r > len(iterable)`
**Explanation:** When the length `r` you ask for is greater than the number of elements, no permutations are possible — Python returns an empty iterator  
**Problem statement:** Handle case where user mistakenly asks for a permutation of length greater than the size of the input  
```python
from itertools import permutations

data = [1, 2]
result = list(permutations(data, 3))
print(result)
```
Output:
```python
[]
```
This prevents errors and is handled gracefully


## 14. Empty Iterable / Edge Case `[]`
**Explanation:** If you pass an empty list or string, only one permutation exists: the empty tuple. This is logical, as the number of ways to arrange zero items is 1 (0! = 1).    
**Problem statement:** Handle edge case where input list or string is empty.  
```python
from itertools import permutations

print(list(permutations([])))        # Output: [()]
print(list(permutations([], 0)))     # Output: [()]
print(list(permutations([], 1)))     # Output: []
```
Output:
```python
[()]
[()]
[]
```



## 15. Using in Comparison with Next Permutation Logic
**Explanation:** In some algorithm problems (like generating the next lexicographic permutation), `itertools.permutations()` can be used to validate correctness by generating all permutations and checking where your current permutation stands.  
**Problem statement:** Verify that a manually implemented “next permutation” function gives correct results using permutations.  
```python
from itertools import permutations

arr = [1, 2, 3]
all_perms = list(permutations(arr))
curr = (1, 2, 3)
idx = all_perms.index(curr)
print("Next permutation:", all_perms[idx + 1])
```
Output:
```python
Next permutation: (1, 3, 2)
```
This is a brute-force way to test correctness of algorithms like next_permutation() in C++ STL or your own logic.

## 16. Convert Iterator to List Safely
**Explanation:** `itertools.permutations()` returns an iterator, not a list. If you want to store or re-use all permutations, you must convert it to a list first — otherwise the iterator is consumed after one loop  
**Problem statement:** Generate all permutations of `[1, 2, 3]` and store them for later access or multiple uses.
```python
from itertools import permutations

data = [1, 2, 3]

# Safe conversion
perm_list = list(permutations(data))
print(perm_list)        # List of all 3! = 6 permutations

# Now you can re-use
print(perm_list[2])     # Access 3rd permutation
```
Output:
```python
[(1, 2, 3), (1, 3, 2), (2, 1, 3), (2, 3, 1), (3, 1, 2), (3, 2, 1)]
(2, 1, 3)
```
Important: If you don’t convert it, you can only loop once — the iterator gets exhausted.


## 17. In-place Usage with Generators (Not Storing)
**Explanation:** If memory is a concern (especially when n! becomes huge), don't store permutations — just loop through them on-the-fly. This saves memory using the lazy generator nature of `itertools.permutations()`.  
**Problem statement:** Loop through all permutations of a large input (e.g. 8 elements), without storing them, for efficient checking.  
```python
from itertools import permutations

data = [1, 2, 3, 4]

# No list() used — memory efficient
for p in permutations(data):
    print(p)
```
Output:
```python
(1, 2, 3, 4)
(1, 2, 4, 3)
...
(4, 3, 2, 1)
```
Great for use in brute-force checking problems like password cracking or puzzle solving


## 18. Unique Permutations in Coding Platforms (with Duplicates in Input)
**Explanation:** When the input has duplicate elements, `itertools.permutations()` will include repeated results. Most platforms expect only unique permutations  
To fix this:  
- Use set(permutations(...)) to remove duplicates.
- Or use a backtracking approach with used[] flag to generate unique permutations.

**Problem statement:** Generate all unique permutations of `[1, 1, 2]`  
Example using `set()`:  
```python
from itertools import permutations

data = [1, 1, 2]

# Remove duplicate tuples using set
unique_perms = set(permutations(data))
for p in unique_perms:
    print(p)
```
Output (order may vary due to `set`):
```python
(1, 2, 1)
(2, 1, 1)
(1, 1, 2)
```
- Interview problems often assume distinct outputs, even with repeated elements.
- Alternative (Leetcode-style): Use custom backtracking with visited array to avoid duplicates without using set.
