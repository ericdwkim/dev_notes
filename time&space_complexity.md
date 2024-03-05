# Time & Space Complexity - Concepts & Terminology

## Memoization
- 
- an optimization technique
- caching system to trade space (memory) for time (faster execution) for instances where a given input and output are deterministic
- typically used for expensive functions, such as recursive functions

Leveraging a hashtable `memo` for faster lookups
```python
def fibonacci(n, memo={}):
    """Compute the nth Fibonacci number using memoization."""
    if n in memo:
        return memo[n]  # Return the cached result if it exists
    if n <= 1:
        return n  # Base cases: fib(0) = 0, fib(1) = 1
    # Store the result in the memo dictionary to avoid recalculating
    memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo)
    return memo[n]

# Example usage
print(fibonacci(10))  # Output: 55

```
In this example, fibonacci function calculates the nth Fibonacci number and uses a dictionary named memo to store the results of each calculation it performs. When the function is called, it first checks if the result for n is already in memo. If so, it returns the cached result, avoiding the need for a redundant calculation. If not, it calculates the value, stores it in memo, and returns it. This drastically reduces the number of calculations needed as n increases, demonstrating the effectiveness of memoization in optimizing recursive function calls.

With memoization time complexity would be either `O(n)` if `n` has not been previously calculated or `O(1)` if `n` has already been calculated and stored in `memo`

The space complexity would be `O(n)` with or w/o memoization, but the key difference is that _with_ memoization, the space complexity can be constant time `O(1)` if returning `n` that has already been previously calculated by searching through the hashtable `memo`. Meanwhile, _without_ memoization, there is no added computational efficiency despite having the same `O(n)` space complexity. This is because the space complexity of a naive recursive fibonacci function (without memoization) is dependent on the maximum depth of the **call stack**. 

Take for instance the following implementation without memoization:

```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)
```
Each call to fibonacci results in two further calls (to `fibonacci(n-1)` and `fibonacci(n-2)`), except for the base cases.
The maximum depth of the call stack occurs along the "leftmost" path of the recursion tree, going from `fibonacci(n)` down to `fibonacci(0)` or `fibonacci(1)`, which results in `O(n)` recursive calls being stacked at most.

