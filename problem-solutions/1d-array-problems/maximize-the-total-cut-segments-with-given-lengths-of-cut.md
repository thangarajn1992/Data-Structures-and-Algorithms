# Maximize The total Cut Segments with given lengths of cut

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/cutted-segments1642/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given an integer **N** denoting the Length of a line segment. You need to cut the line segment in such a way that the cut length of a line segment each time is either **x** , **y** or **z**. Here x, y, and z are integers. After performing all the cut operations, your **total number of cut segments must be maximum**.

**Example 1:**

```text
Input:
N = 4
x = 2, y = 1, z = 1
Output: 4
Explanation:Total length is 4, and the cut
lengths are 2, 1 and 1.  We can make
maximum 4 segments each of length 1.
```

**Example 2:**

```text
Input:
N = 5
x = 5, y = 3, z = 2
Output: 2
Explanation: Here total length is 5, and
the cut lengths are 5, 3 and 2. We can
make two segments of lengths 3 and 2.
```

**Expected Time Complexity** : O\(N\)  
**Expected Auxiliary Space**: O\(N\)

**Constraints**  
 1 &lt;= N, x, y, z &lt;= 10^4

### Solution

#### Dynamic Programming Approach

```cpp
class Solution
{
    public:
    int maximizeTheCuts(int n, int x, int y, int z)
    {
        vector<int>  dp(n+1, -1);
        dp[0] = 0;
        for(int i = 0; i <= n; i++)
        {
            if(dp[i] == -1)
                continue;
            if(i+x <= n)
                dp[i+x] = max(dp[i+x], dp[i]+1);
            if(i+y <= n)
                dp[i+y] = max(dp[i+y], dp[i]+1);
            if(i+z <= n)
                dp[i+z] = max(dp[i+z], dp[i]+1);   
        }
        return (dp[n] == -1)? 0 : dp[n]; 
    }
};
```



