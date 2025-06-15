## Binary and  Modular Exponentiation

### Binary Exponentiation 
Efficient method to compute `a^b` in `O(log b)` time.

1. Recursive Method
- **Time Complexity**: O(log b)  
- **Space Complexity**: O(log b) (due to recursion stack)

```python
def binPow(a, b):
    if b == 0:
        return 1
    
    res = binPow(a, b // 2)
    if b % 2:
        return res * res * a
    else:
        return res * res
```

2. Iterative (Bit Manipulation)
- **Time Complexity**: O(log b)  
- **Space Complexity**: O(1)  
- More practical than recursion due to zero stack overhead.

```python
def binPow(a, b):
    res = 1
    while b > 0:
        if b & 1:
            res *= a
        a *= a
        b >>= 1
    return res
```

---

### Modular Exponentiation
Used to compute `(a^b) % m` efficiently.

- **Time Complexity**: O(log b)  
- **Space Complexity**: O(1)

```python
def binPow(a, b, m):
    res = 1
    a %= m
    while b > 0:
        if b & 1:
            res = (res * a) % m
        a = (a * a) % m
        b >>= 1
    return res
```