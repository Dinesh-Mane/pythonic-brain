# Common ways to define Infinite value (`∞`)
## 1. Using `float('inf')` and `float('-inf')`
This is the most standard and Pythonic way.
```python
INF = float('inf')
NEG_INF = float('-inf')

print(INF > 10**18)     # True
print(NEG_INF < -10**18)  # True
```

## 2. Using `math.inf` and `-math.inf`
Same as `float('inf')`, but comes from the math module.
```python
import math

INF = math.inf
NEG_INF = -math.inf
```
Internally, `math.inf == float('inf')` → both are identical.

## 3. Using a Very Large Integer (`10**9`, `10**18`)
In CP, sometimes `inf` is mocked using large integers due to performance or input constraints.
```python
INF = int(1e9)         # 1000000000
BIG_INF = int(1e18)    # 1000000000000000000
```
Use only when you're sure the problem values never go beyond this.

## 4. Using `sys.maxsize`
This gives the maximum integer value for your system (usually 2⁶³ - 1 on 64-bit systems).
```python
import sys

INF = sys.maxsize      # 9223372036854775807 (on most systems)
NEG_INF = -sys.maxsize
```

## 5. Using `decimal.Decimal('Infinity')`
Used in financial or high-precision applications.
```python
from decimal import Decimal

INF = Decimal('Infinity')
NEG_INF = Decimal('-Infinity')
```
Slower than `float('inf')`, not used in DSA/CP usually.


## Not Recommended (But Seen in Some Codebases):
Hardcoded string:
```python
INF = "inf"  # This is a string, so mathematical comparisons will fail
```
