# Time Complexity

**How to Analyse Time Complexity?**

Running time of an algorithm depends on various factors

* Single vs Multiple Processor
* Read & Write Speed
* 32-bit vs 64- bit Architecture
* Configuration of the Machine
* Input

When we say Time Complexity of a program, we are generally concerned about the **"input"** factor. How various input affects our time complexity. **Time Complexity is defined as a function of input.**

### Constant Time Complexity O\(1\)

If a program takes constant time irrespective of input, then it is said to have constant time complexity

```cpp
int add(int a, int b)
    return a+b;
```

Irrespective of input, this function will always take constant time in a given system.

### Linear Time Complexity O\(n\)

If a program execution time linearly increases with the increase in input size, then it is said to have linear time complexity

```cpp
int sum(int n, vector<int>&nums)
{
    int total = 0;
    for(int num = 0; num < nums.size(); num++)
        total += nums[num];
    return total;
}
```

As the size of the input list increases, the number of addition increases linearly.

### Quadratic Time Complexity O\(n^2\)

As input increases, the execution time increases quadratic.

```cpp
int sum(int n, vector<vector<int>> &matrix)
{
    int total = 0;
    for(int row = 0; row < matrix.size(); row++)
        for(int col = 0; col < matrix[0].size(); col++)
            total += matrix[row][col];
    return total; 
}
```

## Asymptotic Notations  

### Big O Notation

As we seen in previous examples, there were some constant statement even in linear and quadratic complexity, but we ignore the lower elements, because as n -&gt; ∞ these lower constants doesnt matter and only the higher elements that depends on n matters. In other words, we ignore the lower elements that is part of execution time and only consider the  higher factors that depends on size of input 'n'.

We try to form various complexities into sets. 

`O(G(n)) = { f(n) : there exists constants C and n0 such that f(n) <= C * G(n) for n >= n0 }` 

All f\(n\) that satisfies this condition can be grouped into the set G\(n\)

Big O =&gt;  Upper bound of rate of growth of time

Eg: `f(n) = 5n^2 + 2n + 1, G(n) = n^2`

`f(n) <= 8n^2  , so C = 8, n0 = 1`

### Omega Notation \(Ω\)

`Ω(G(n)) = { f(n) : there exists constants C and n0 such that C * G(n) <= f(n) for n >= n0`

Eg: `f(n) = 5n^2 + 2n + 1, G(n) = n^2`

`f(n) >=  5n^2 for n >= 0  C = 5, n0 = 0`

Omega =&gt; Lower Bound of Growth of Rate of Time

### Theta Notation \(ø\)

`ø(G(n)) = { f(n) : there exists constants C1, C2 and n0 such that  C1*G(n) <= f(n) <= C2 * G(n)     for n>=n0 }`

Eg: `f(n) = 5n^2 + 2n + 1, G(n) = n^2`

`5n^2 <= f(n) <= 8n^2 for n >= 0  C1 = 5, C2 = 8, n0 = 0`

Theta =&gt; Tight Bound.

Always good to evaluate the time complexity of algorithm in theta notation.

## General Rules

We analyze time complexity for 

1. Very Large Input Size
2. Worst Case Scenario

For `T(n) = n^3 + 3n^2 + 4n + 2`  , for larger n, the lower degree becomes insiginicant and it approximated to `T(n) ~ n^3 for n -> ∞`

**Rule 1: Big O notation for polynomial expression:**

1. Drop all lower order elements
2. Drop all constant multipliers
3. Drop log\(n\) as well since for higher n, log\(n\) is insignificant compared to 'n' in expression `n + log(n)`  

**Rule 2: Running Time of Algorithm**

Running time of an algorithm is sum of run-time of fragments in the algorithm









