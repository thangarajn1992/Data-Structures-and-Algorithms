# 0 - 1 Knapsack Problem

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/0-1-knapsack-problem0945/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Flipkart](../../company-based-lists/flipkart.md)

### Problem Statement

You are given weights and values of **N** items, put these items in a knapsack of capacity **W** to get the maximum total value in the knapsack. Note that we have only **one quantity of each item**.  
 In other words, given two integer arrays **val\[0..N-1\]** and **wt\[0..N-1\]** which represent values and weights associated with **N** items respectively. Also given an integer W which represents knapsack capacity, find out the maximum value subset of **val\[\]** such that sum of the weights of this subset is smaller than or equal to **W.** You cannot break an item, **either pick the complete item or don’t pick it \(0-1 property\)**.

**Example 1:**

```text
Input:
N = 3
W = 4
values[] = {1,2,3}
weight[] = {4,5,1}
Output: 3
```

**Example 2:**

```text
Input:
N = 3
W = 3
values[] = {1,2,3}
weight[] = {4,5,6}
Output: 0
```

**Expected Time Complexity:** O\(N\*W\).  
**Expected Auxiliary Space:** O\(N\*W\)

**Constraints:**  
 1 ≤ N ≤ 1000  
 1 ≤ W ≤ 1000  
 1 ≤ wt\[i\] ≤ 1000  
 1 ≤ v\[i\] ≤ 1000

### Solution

```cpp
class Solution
{
    public:
    //Function to return max value that can be put in knapsack of capacity W.
    int knapSack(int W, int wt[], int val[], int n) 
    { 
        vector<int> dp(W + 1, 0);

        for (int i = 1; i < n + 1; i++) 
        {
            for (int w = W; w >= 0; w--) 
            {
                if (wt[i - 1] <= w)
                    dp[w] = max(dp[w], dp[w - wt[i - 1]] + val[i - 1]);
            }
        }
        return dp[W]; // returning the maximum value of knapsack
    }
};
```

