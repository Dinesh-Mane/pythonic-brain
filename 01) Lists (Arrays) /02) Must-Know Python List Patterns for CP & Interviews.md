# 1. Sliding Window Pattern
Fixed/Variable size window madhe subarrays process karne.
```python
# Find max sum of k consecutive elements
def max_sum_subarray(arr, k):
    curr_sum = sum(arr[:k])
    max_sum = curr_sum
    for i in range(k, len(arr)):
        curr_sum += arr[i] - arr[i-k]
        max_sum = max(max_sum, curr_sum)
    return max_sum

print(max_sum_subarray([1, 2, 3, 4, 5, 6, 7], 3))  # 18 (5+6+7)
```
# 2. Two Pointers Technique
Use 2 pointers (`left`, `right`) to shrink or expand range.
```python
# Check if array has a pair with target sum
def has_pair(arr, target):
    arr.sort()   # remember: arr sorted asayla pahije
    l, r = 0, len(arr) - 1
    while l < r:
        total = arr[l] + arr[r]
        if total == target: return True
        elif total < target: l += 1
        else: r -= 1
    return False

print(has_pair([1, 4, 6, 8], 10))  # True
```
# 3. Prefix Sum
Fast range-sum queries using precomputed prefix array.
```python
arr = [2, 4, 6, 8]
prefix = [0]
for num in arr:
    prefix.append(prefix[-1] + num)

# Sum from index 1 to 3 → (4+6+8)
print(prefix[4] - prefix[1])  # 18
```
# 4. List Comprehension (Fast Filtering/Mapping)
```python
# Square of even numbers
arr = [1, 2, 3, 4]
evens_squared = [x**2 for x in arr if x % 2 == 0]
print(evens_squared)  # [4, 16]
```
# 5. List Reversal / Palindrome Check
```python
# Palindrome check
arr = [1, 2, 3, 2, 1]
print(arr == arr[::-1])  # True
```
# 6. Finding Duplicates Using Set
```python
arr = [1, 2, 3, 2]
seen = set()
for x in arr:
    if x in seen:
        print("Duplicate found:", x)
        break
    seen.add(x)
```
# 7. Sorting by Custom Key
```python
arr = ["apple", "banana", "kiwi"]
arr.sort(key=len)
print(arr)  # ['kiwi', 'apple', 'banana']
```
# 8. Binary Search on Sorted List
Use `bisect` module.
```python
import bisect
arr = [10, 20, 30, 40]
print(bisect.bisect_left(arr, 25))  # 2 (insert point)
```
# 9. Frequency Count using Dictionary
```python
arr = [1, 2, 2, 3]
freq = {}
for num in arr:
    freq[num] = freq.get(num, 0) + 1
print(freq)  # {1: 1, 2: 2, 3: 1}
```
# 10. List Flattening (2D → 1D)
```python
matrix = [[1, 2], [3, 4]]
flat = [x for row in matrix for x in row]
print(flat)  # [1, 2, 3, 4]
```
# 11. Kadane’s Algorithm (Max Subarray Sum)
```python
arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
max_sum = curr = arr[0]
for x in arr[1:]:
    curr = max(x, curr + x)
    max_sum = max(max_sum, curr)
print(max_sum)  # 6
```
# 12. List Rotation
```python
arr = [1, 2, 3, 4]
k = 2
# Right rotate
rotated = arr[-k:] + arr[:-k]
print(rotated)  # [3, 4, 1, 2]
```
# 13. Enumerate with Index
```python
arr = ['a', 'b', 'c']
for i, val in enumerate(arr):
    print(f"Index {i}: {val}")
```
# 14. Using zip() with two lists
```python
names = ["Ram", "Sham"]
scores = [80, 90]
for name, score in zip(names, scores):
    print(name, score)
```
# 15. Finding Second Largest Element
```python
arr = [4, 1, 2, 9, 7]
first = second = float('-inf')
for num in arr:
    if num > first:
        second = first
        first = num
    elif num > second and num != first:
        second = num
print(second)  # 7
```
# 16. Monotonic Stack / Monotonic Queue
Fast track for next greater/smaller element problems.  
Use Case: Stock span, temperatures, histograms, circular arrays
```python
# Next Greater Element
def next_greater(arr):
    res = [-1] * len(arr)
    stack = []
    for i in range(len(arr)):
        while stack and arr[i] > arr[stack[-1]]:
            res[stack.pop()] = arr[i]
        stack.append(i)
    return res

print(next_greater([2, 1, 2, 4, 3]))  # [4, 2, 4, -1, -1]
```
# 17. Difference Array Technique (Range Updates in O(1))
Use when multiple range updates are needed.
```python
# Range update using difference array
def range_update(arr_len, updates):
    diff = [0] * (arr_len + 1)
    for start, end, val in updates:
        diff[start] += val
        if end + 1 < len(diff):
            diff[end + 1] -= val
    
    res = []
    curr = 0
    for i in range(arr_len):
        curr += diff[i]
        res.append(curr)
    return res

print(range_update(5, [(1, 3, 2), (2, 4, 3)]))  # [0, 2, 5, 5, 3]
```
# 18. Cycle Detection in List using Floyd’s Tortoise-Hare
Used in linked list cycle problems, but applicable in array-index-based jumps too.
```python
def has_cycle(nums):
    slow = fast = 0
    while True:
        slow = nums[slow]
        fast = nums[nums[fast]]
        if slow == fast:
            return True
        if fast >= len(nums) or nums[fast] >= len(nums):
            return False

# Index jump based example
print(has_cycle([1, 2, 3, 4, 0]))  # True (cycle)
```
# 19. Two-Pass Traversal
When solution needs first forward loop, then backward loop (or vice-versa).
```python
# Find days until warmer temperature
def warmer_days(temps):
    res = [0] * len(temps)
    stack = []
    for i in range(len(temps)-1, -1, -1):
        while stack and temps[i] >= temps[stack[-1]]:
            stack.pop()
        if stack:
            res[i] = stack[-1] - i
        stack.append(i)
    return res

print(warmer_days([73, 74, 75, 71, 69, 72, 76, 73]))
# [1, 1, 4, 2, 1, 1, 0, 0]
```
# 20. Greedy Local Optimal from List
Try locally best choice (e.g., jump game, interval scheduling)
```python
# Can jump to end?
def can_jump(nums):
    max_reach = 0
    for i, val in enumerate(nums):
        if i > max_reach:
            return False
        max_reach = max(max_reach, i + val)
    return True

print(can_jump([2,3,1,1,4]))  # True
```
# 21. Backtracking on List / Permutations
For generating all possible combinations, permutations.
```python
# Permutations
def permute(nums):
    res = []
    def backtrack(path, rem):
        if not rem:
            res.append(path)
            return
        for i in range(len(rem)):
            backtrack(path + [rem[i]], rem[:i] + rem[i+1:])
    backtrack([], nums)
    return res

print(permute([1,2,3]))
```
# 22. Bucket / Frequency Based List Tricks
Often used in counting, group-by or sorting by frequency.
```python
from collections import Counter

def top_k(nums, k):
    freq = Counter(nums)
    buckets = [[] for _ in range(len(nums) + 1)]
    for num, count in freq.items():
        buckets[count].append(num)

    res = []
    for i in range(len(buckets)-1, -1, -1):
        for num in buckets[i]:
            res.append(num)
            if len(res) == k:
                return res

print(top_k([1,1,1,2,2,3], 2))  # [1,2]
```
# 23. Bitmasking on Lists
Combinations/subsets problems jithe performance tight asel tithe bitmasking is fastest way.  
Use case: Subsets, XOR problems, DP with state compression  
```python
# All subsets using bitmask
arr = [1, 2, 3]
n = len(arr)
for i in range(1 << n):  # 2^n
    subset = [arr[j] for j in range(n) if (i >> j) & 1]
    print(subset)
```
# 24. Two Dimensional Prefix Sum (Matrix Based Lists)
2D list sathi fast range sum queries (O(1)).
```python
# 2D Prefix Sum
matrix = [
    [1, 2],
    [3, 4]
]
rows, cols = len(matrix), len(matrix[0])
prefix = [[0] * (cols + 1) for _ in range(rows + 1)]

for i in range(rows):
    for j in range(cols):
        prefix[i+1][j+1] = matrix[i][j] + prefix[i][j+1] + prefix[i+1][j] - prefix[i][j]

# Query sum of submatrix from (0,0) to (1,1)
print(prefix[2][2])  # 10
```
# 25. Meet in the Middle
Used when list is big (e.g., n = 30) and you need subset combinations.  
Use case: Subset sum, knapsack where brute force is slow  
```python
# Idea: Split array in 2 halves, generate all subset sums of both
# Then combine smartly using binary search / hashing
```
# 26. Deque-Based Sliding Window (for max/min)
Instead of normal sliding window, deque gives O(1) max/min window.  
```python
from collections import deque

# Sliding window max
def max_window(arr, k):
    dq = deque()
    res = []
    for i in range(len(arr)):
        while dq and dq[-1][0] < arr[i]:
            dq.pop()
        dq.append((arr[i], i))

        if dq[0][1] <= i - k:
            dq.popleft()
        
        if i >= k - 1:
            res.append(dq[0][0])
    return res

print(max_window([1,3,-1,-3,5,3,6,7], 3))
# [3,3,5,5,6,7]
```
# 27. Zigzag / Diagonal Traversal in Lists
Used in 2D list based questions: like matrix problems.  
```python
# Diagonal traversal of matrix
matrix = [[1,2,3],[4,5,6],[7,8,9]]
for s in range(len(matrix)*2 - 1):
    for i in range(len(matrix)):
        j = s - i
        if 0 <= j < len(matrix[0]):
            print(matrix[i][j], end=' ')
```
# 28. Union-Find / Disjoint Set on List
Use list to track `parent[]` and `rank[]`. 
Use case: Connected components, cycle detection, Kruskal's MST
```python
# Basic union-find with path compression
parent = list(range(5))

def find(x):
    if parent[x] != x:
        parent[x] = find(parent[x])
    return parent[x]

def union(x, y):
    parent[find(x)] = find(y)
```
# 29. Delta Counting Pattern (Line Sweep)
List madhe changes track karayche astil (like number of people in range), use delta diff
```python
# Example: find max number of overlapping intervals
events = [(1, 5), (2, 6), (4, 7)]
timeline = [0]*10
for start, end in events:
    timeline[start] += 1
    timeline[end] -= 1

active = 0
max_active = 0
for val in timeline:
    active += val
    max_active = max(max_active, active)

print(max_active)  # 3
```
