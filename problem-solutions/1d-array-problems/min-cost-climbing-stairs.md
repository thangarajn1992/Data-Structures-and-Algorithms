# Min Cost Climbing Stairs

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/min-cost-climbing-stairs/1#)

### Companies

* 
### Problem Statement

Given an array of integers **cost\[\]** of length **N**, where **cost\[i\]** is the cost of the ith step on a staircase. Once the cost is paid, you can either climb one or two steps. You can either start from the step with index 0, or the step with index 1. Return the minimum cost to reach the top of the floor.  
  
 **Example 1:**

```text
Input:
N = 3
cost[] = {10, 15, 20}
Output:
15
Explanation:
Cheapest option is to start at cost[1],
pay that cost, and go to the top.
```

  
 **Example 2:**

```text
Input:
N = 10
arr[] = {1, 100, 1, 1, 1, 100, 1, 1, 100, 1}
Output:
6
Explanation:
Cheapest option is to start on cost[0], 
and only step on 1s, skipping cost[3].
```

**Expected Time Complexity:** O\(N\).  
**Expected Auxiliary Space:** O\(1\).  
  
 **Constraints:**  
 2 ≤ N ≤ 10^3  
 0 ≤ cost\[i\] ≤ 999

### Solution

#### Dynamic Programming/Memoization

```cpp
class Solution {
  public:
    int minCostClimbingStairs(vector<int>&cost ,int N) {
        int two_step = 0, one_step = 0;
        for(int stair = N-1; stair >= 0; stair--)
        {
            int cur_step  = min(two_step, one_step) + cost[stair];
            two_step = one_step;
            one_step = cur_step;
        }        
        return min(two_step, one_step);
    }
};
```

