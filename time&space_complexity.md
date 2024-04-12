# Time & Space Complexity - Concepts & Terminology

## Memoization

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

## Amortized Time Complexity
- tl;dr: "average time" complexity of a given measure; the middle ground efficiency 
- This concept is about how for given algo, there are many variances of its performance ranging from the worst to the best case scenarios that it is a better way to conceptualize the algo's efficiency as the "average"
- For example, **dynamic arrays**:
  - pushing a value to a dynamic array will be O(1) - constant time; makes sense b/c it is the same as popping from or pushing to any array
  - when a dynamic array needs to be increased, a brand new array is created with all the values from the old (too small) array being pushed into the new array; this new array's length gets doubled in size to allocate more space required for extra values 
  - why the length of the array gets _doubled_ in size and not just enough to account for the extra values (say 1 or 2 extra slots) or a ton more slots is due to a mathematical proof concept called`Power Series` 


### Adding one additional slot each time:

**Operation**: Each time a new element is added, the array is expanded by one slot.

**Efficiency Issue**: This method requires reallocating space and copying the existing elements to a new memory area each time a new element is added. This makes each insertion operation O(n), where n is the current number of elements in the array. This happens because each insertion needs to copy all existing elements to the new array location.

**Amortized Analysis**: If you add n items, you end up performing an operation that takes 1 time for the first item, 2 times for the second item, 3 times for the third item, and so on, up to n times for the nth item. The total time for all insertions is 

```
1 + 2 + 3 + ... + n = n(n + 1) / 2
```
and when divided by n (to find the average time per operation), the complexity is `O(n)`. Hence, each operation, when considered with all others, also has an average complexity of O(n).

### Adding a ton of new slots each time:

**Operation**: Instead of just doubling, suppose the array size is multiplied by a much larger constant or a huge number of slots are added each time it grows.

**Efficiency Issue**: While this strategy reduces the frequency of reallocations (thus reducing the number of costly copy operations), it has significant drawbacks:

**Memory Waste**: This method can lead to a substantial waste of memory if the allocated space far exceeds the actual number of items stored. This is inefficient, particularly when memory resources are limited or when the array uses a lot of memory relative to the data it actually needs to store.

**Cost Analysis**: Although the number of operations required to copy elements might decrease, the massive allocation of memory still requires time and can degrade performance, especially in systems where memory allocation is costly.

**Amortized Analysis**: Even though the average cost of insertion might remain low if considered over a large number of operations (due to less frequent reallocations), the practical inefficiencies due to memory waste make this approach less desirable.

### Comparison and Practical Impact:

The strategy of doubling the size of the array strikes a balance between these extremes. It ensures that space is efficiently utilized and that the cost of copying elements is spread out over many insertions, leading to an amortized time complexity of `O(1)` _per insertion_. This means that while some insertions might be expensive (those that require resizing and copying), many others are very cheap (simple additions), and on average, the cost is constant.
The doubling method also minimizes the number of times the array needs to be resized as it grows, which is a significant factor in maintaining good performance as n becomes large.