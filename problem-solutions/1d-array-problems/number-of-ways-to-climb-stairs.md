# Number of ways to Climb Stairs

### Sources

* [Leetcode 70](https://leetcode.com/problems/climbing-stairs/)

### Companies

### Problem Statement

You are climbing a staircase. It takes `n` steps to reach the top. Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

**Example 1:**

```text
Input: n = 2
Output: 2
Explanation: 
There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

**Example 2:**

```text
Input: n = 3
Output: 3
Explanation: 
There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

**Constraints:**

* `1 <= n <= 45`

### Solution

### Dynamic Programming/Memoization

```cpp
class Solution {
public:
    int climbStairsiter(int n, int cur, vector<int>& possibilities)
    {
        if(cur == n)
            return 1;
        if(cur > n)
            return 0;
        if(possibilities[cur])
            return possibilities[cur];
        possibilities[cur] += climbStairsiter(n, cur+1, possibilities);
        possibilities[cur] += climbStairsiter(n, cur+2, possibilities);
        return possibilities[cur];
    }
    int climbStairs(int n) {
        vector<int> possibilities(n, 0);
        return climbStairsiter(n, 0, possibilities);
    }
};
```

