## Prefix Sum
### 1-D Prefix Sum
Used to find range sum.<br>
Ex: 
- Input array nums of size N.
- Sum of Range [x1, x2]

```python
# Initialize Prefix Sum
ps = [0] * (N+1)

# Fill ps array
for i in range(1, N+1):
    ps[i] = ps[i-1] + nums[i-1]

# Range Sum
print(ps[x2+1] - ps[x1])
```

**Time Complexity**:
- Preprocessing: O(N)
- Range Query: O(1)

**Space Complexity**: O(N)

---

### 2-D Prefix Sum
Used to find submatrix sum.<br>
Ex: 
- Input matrix of size MxN.
- Submatrix Sum: (x1, y1) top-left coordinate, (x2, y2) bottom-left coordinate.

```python
# Initialize Prefix Sum
ps = [[0]*(N+1) for _ in range(M+1)]

# Fill ps array
for i in range(1, M+1):
    for j in range(1, N+1):
        ps[i][j] = matrix[i-1][j-1] + ps[i-1][j] + ps[i][j-1] - ps[i-1][j-1]

# Submatrix Sum
sub_sum = ps[x2+1][y2+1] + ps[x1][y1] - ps[x1][y2+1] - ps[x2+1][y1]
print(sub_sum)
```

**Time Complexity**:
- Preprocessing: O(M×N)
- Query: O(1)

**Space Complexity**: O(M×N)

---

## Difference Arrays
1D lazy range update.<br>
Ex:
- Input: Queries [start, end], with maximum size N.
- Find number of queries at x.
- Make sure of inclusion/exlusion of each index.

**Code**:
```python
d = [0] * (N + 2)  # N+2 to avoid out-of-bounds

# Process Queries
for start, end in queries:
    d[start] += 1
    d[end+1] -= 1

# Apply Prefix Sum
for i in range(1, N+1):
    d[i] += d[i-1]

print(d[1:N+1])
```

**Time Complexity**:
- Update: O(Q) for Q queries
- Prefix Sum Application: O(N)

**Space Complexity**: O(N)
