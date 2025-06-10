## Prefix Sum
### 1-D PRefix Sum
Used to find range sum.
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
print(ps[x2+1]-ps[x1])
```

### 2-D PRefix Sum
Used to find submatrix sum.
Ex: 
- Input matrix of size MxN.
- Submatrix Sum: (x1, y1) top-left coordinate, (x2, y2) bottom-left coordinate.

```python
# Initialize Prefix Sum
ps = [[0]*(N+1) for i in range(M+1)]

# Fill ps array
for i in range(1, M+1):
    for j in range(1, N+1):
        ps[i][j] = matrix[i-1][j-1] + ps[i-1][j] + ps[i][j-1] - ps[i-1][j-1]

# Submatrix Sum
sub_sum = ps[x2+1][y2+1] + ps[x1][y1] - ps[x1][y2+1] - ps[x2+1][y1]
print(sub_sum)
```

## Difference Arrays
1D lazy range update.
Ex:
- Input: Queries [start, end], with maximum size N.
- Find number of queries at x.
- Make sure of inclusion/exlusion of each index.

```python
d = [0] * (N+2)
# Process Queries
for start, end in queries:
    d[start] += 1
    d[end+1] -= 1

# Apply prefix sum
for i in range(1, N+1):
    d[i] += d[i-1]

print(d)
```
