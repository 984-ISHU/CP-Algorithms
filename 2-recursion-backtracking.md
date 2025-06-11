## Recursion

### 1. nth Item in Fibonacci Sequence

#### Iterative Solution
- **Time Complexity:** O(n)
- **Space Complexity:** O(1)
```python
def fibo(n):
    if n < 2:
        return n

    a, b = 0, 1
    for i in range(2, n + 1):
        a, b = b, a + b
    return b
```

#### Recursion with Memoization
- **Time Complexity:** O(n)
- **Space Complexity:** O(n) for recursion stack and memo dictionary
```python
def fibo(n, memo={}):
    if n in memo:
        return memo[n]
    memo[n] = fibo(n - 1) + fibo(n - 2)
    return memo[n]

# Initialize memo
memo = {0: 0, 1: 1}
fibo(10, memo)
```

---

### 2. Factorial of a Non-Negative Integer

#### Iterative Method
- **Time Complexity:** O(n)
- **Space Complexity:** O(1)
```python
def factorial(n):
    res = 1
    for i in range(2, n + 1):
        res *= i
    return res
```

#### Recursive Method
- **Time Complexity:** O(n)
- **Space Complexity:** O(n) due to call stack
```python
def factorial(n):
    if n < 2:
        return 1
    return n * factorial(n - 1)
```

---

## Backtracking

### 1. Permutations

#### Using `itertools.permutations`
- **Time Complexity:** O(n!)
- **Space Complexity:** O(n!)
```python
from itertools import permutations
# Generate permutations of length r
p = permutations(data, r)
```

#### Backtracking (Unique Array)
- **Time Complexity:** O(n!)
- **Space Complexity:** O(n!) for storing results
```python
def permutations(arr):
    res = []

    def backtrack(start):
        if start == len(arr):
            res.append(arr[:])
            return

        for i in range(start, len(arr)):
            arr[start], arr[i] = arr[i], arr[start]
            backtrack(start + 1)
            arr[start], arr[i] = arr[i], arr[start]

    backtrack(0)
    return res
```

#### Backtracking (With Duplicates)
- Sort input + skip duplicates
- **Time Complexity:** O(n! / k!) where k is the count of duplicate elements
- **Space Complexity:** O(n!)
```python
def permutations(arr):
    res = []
    arr.sort()

    def backtrack(path, used):
        if len(path) == len(arr):
            res.append(path[:])
            return

        for i in range(len(arr)):
            if used[i]:
                continue
            if i > 0 and arr[i] == arr[i - 1] and not used[i - 1]:
                continue

            used[i] = True
            path.append(arr[i])
            backtrack(path, used)
            path.pop()
            used[i] = False

    backtrack([], [False] * len(arr))
    return res
```

---

### 2. Combinations

#### Using `itertools.combinations`
- Lexicographically sorted
- Position matters
- **Time Complexity:** O(nCr)
```python
from itertools import combinations
c = combinations(data, r)
```

#### Backtracking
- **Time Complexity:** O(nCr)
- **Space Complexity:** O(nCr)
```python
def combinations_r(arr, r):
    n = len(arr)
    res = []

    def backtrack(start, path):
        if len(path) == r:
            res.append(path[:])
            return

        for i in range(start, n):
            path.append(arr[i])
            backtrack(i + 1, path)
            path.pop()

    backtrack(0, [])
    return res
```

#### Bitmask
- **Time Complexity:** O(2^n)
- **Space Complexity:** O(2^n)
```python
def combinations_r(arr, r):
    n = len(arr)
    res = []
    for mask in range(1 << n):
        temp = [arr[i] for i in range(n) if (mask >> i) & 1]
        if len(temp) == r:
            res.append(temp)
    return res
```

---

### 3. Powerset

#### Backtracking
- **Time Complexity:** O(2^n)
- **Space Complexity:** O(2^n)
```python
def powerset(arr):
    res = []

    def backtrack(start, path):
        res.append(path[:])
        for i in range(start, len(arr)):
            path.append(arr[i])
            backtrack(i + 1, path)
            path.pop()

    backtrack(0, [])
    return res
```

#### Bitmask
- **Time Complexity:** O(2^n)
- **Space Complexity:** O(2^n)
```python
def powerset(arr):
    n = len(arr)
    res = []
    for mask in range(1 << n):
        temp = []
        for i in range(n):
            if (mask >> i) & 1:
                temp.append(arr[i])
        res.append(temp)

    return res
```


