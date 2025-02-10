# Complexity Analysis

It's important to pay attention to problem constrants. A lot of the times, you can guess the algorithm by looking at the constraints. 

| n | time complexity | name | examples |
| - | - | - | - |
| n ≤ 12 | O(n!) | Factorial time | Creating all permutations of 1 ... n |
| n ≤ 25 | O(2<sup>n</sup>) | Exponential time | Creating all subsets of an array of size n |
| n ≤ 100 | O(n<sup>4</sup>) | | |
| n ≤ 500 | O(n<sup>3</sup>) | Cubic time | |
| n ≤ 10<sup>4</sup> | O(n<sup>2</sup>) | Quadratic time | Slow comparison-based sorting (eg. Bubble Sort, Insertion Sort, Selection Sort) |
| n ≤ 10<sup>6</sup> | O(n log n) | Linearithmic time | Fast comparison-based sorting (eg. Merge Sort) |
| n ≤ 10<sup>8</sup> | O(n) | Linear time | Linear search, 2 pointer approach, sliding window approach |
| n > 10<sup>9</sup> | O(log n) | Logarithmic time | Binary search, finding GCD with Euclidean Algorithm |
| n > 10<sup>9</sup> | O(1) | Constant time | |

In general, the number has to smaller than 10<sup>9</sup> after assigning the max possible constraint in the big O of your algorithm.

It's easy to calculate this with python. See the following for the cubic time example.

```python3
>>> math.log(500**3, 10)
8.096910013008056
```

Reference
- https://codeforces.com/blog/entry/21344
