## Primes and Prime Factorization

### ✅ Check if a Number is Prime
- **Time Complexity:** O(√N)
- **Space Complexity:** O(1)

```python
def isPrime(n):
    if n < 2:
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True
```

---

### ✅ Generate All Prime Numbers Less Than or Equal to N
- **Algorithm:** Sieve of Eratosthenes
- **Time Complexity:** O(N log log N)
- **Space Complexity:** O(N)

```python
def SieveOfEratosthenes(n):
    isPrime = [True] * (n + 1)
    isPrime[0] = isPrime[1] = False

    p = 2
    while p * p <= n:
        if isPrime[p]:
            for i in range(p * p, n + 1, p):
                isPrime[i] = False
        p += 1

    primes = [i for i, val in enumerate(isPrime) if val]
    return primes
```

---

## ✅ Fast Prime Factorization
- **Preprocessing Time Complexity:** O(N log log N)
- **Query Time Complexity (per number):** O(log N)
- **Space Complexity:** O(N)

```python
# Pre-compute smallest prime factor (spf) for every number up to N
N = 10**6
spf = [0] * (N + 1)

def smallestPrimeFactor(N):
    for i in range(2, N + 1):
        spf[i] = i

    for i in range(2, int(N**0.5) + 1):
        if spf[i] == i:  # Check if 'i' is a prime
            for j in range(i * i, N + 1, i):
                if spf[j] == j:
                    spf[j] = i

def findPrimeFactors(n):
    primeFactors = []
    while n > 1:
        x = spf[n]
        primeFactors.append(x)
        n //= x
    return primeFactors
```