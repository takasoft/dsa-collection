## Important Formulas

Permutation = nPr = n! / (n – r)!

Combination = nCr = nPr / r! =  n! / (r! * (n – r)!)

## Pascal's Triangle

O(n^2) Algorithm for constucting Pascal's triangle row given n = the height of the triangle.

```python3
triangleRow = [1]
for _ in range(n-1):
    newRow = [triangleRow[0]]
    for i in range(len(triangleRow)-1):
        newRow.append(triangleRow[i] + triangleRow[i+1])
    newRow.append(triangleRow[-1])
    triangleRow = newRow
```

For n = 5, it will print out `[1, 4, 6, 4, 1]`

Pascal's triangle is related to combinatrics. 

It is possible to calculate the numbers in O(n).

1, 4, 6, 4, 1 is actually 4C0, 4C1, 4C2, 4C3, 4C4. Thus, given `comb` function which computes combination, we can write the following simple algorithm.

```python3
triangleRow = [comb(n-1, i) for i in range(n)]    
```

`math.comb()` is not O(1). Since it involves factorial. To give O(1) efficiency, we need to precompute factorials up to n.

Usually the problem also requires that we return the answer mod some prime. So let's assume we have MOD constant. We then need modular inverse of factorials as well. In python, we can simply use `pow(base, -1, MOD)`.

```python3
factorial = [1]
for i in range(1, n + 1):
    factorial.append(factorial[-1] * i % MOD)
invFactorial = [pow(factorial[-1], -1, MOD)]
for i in reversed(range(1, n + 1)):
    invFactorial.append(invFactorial[-1] * i % MOD)
invFactorial.reverse()
```

Now `comb` function will look like this.

```python3
def comb(n, r):
    return factorial[n] * invFactorial[r] * invFactorial[n – r] % MOD
```
