## Euclidean Algorithm for Calculating GCD
- O(log min(a, b))

### GCD
1. Recursive
```python
def gcd(a, b):
    if b == 0:
        return a
    else:
        return gcd(b, a%b)
```

2. Non-recursive
```python
def gcd(a, b):
    while b:
        a %= b
        a, b = b, a
    return a
```

3. Built-in
```python
from math import gcd
print(gcd(6, 12, 18)) # 6
```

### LCM
1. Using gcd
```python
def lcm(a, b):
    return a * b / gcd(a, b)
```

2. Built-in
```python
from math import lcm
print(lcm(4, 8, 12)) # 24
```


