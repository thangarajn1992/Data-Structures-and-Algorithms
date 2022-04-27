# Minimum elements to change to achieve XOR of array elements higher than given value

### Sources

* [GeeksForGeeks](https://practice.geeksforgeeks.org/problems/7ba682ec660335b1627f2183f63bd2c8a37391ec/1#)

### Companies



### Problem Statement

Given an array **A\[ ]** of **N** integers and an integer **X**. In one operation, you can change the **ith** element of the array to any integer value where **1 ≤ i ≤ N**. Calculate minimum number of such operations required such that the **bitwise** [**AND**](https://en.wikipedia.org/wiki/Bitwise\_operation#AND) of all the elements of the array is strictly greater than **X**.

**Example 1:**

```
Input:
N = 4, X = 2
A[] = {3, 1, 2, 7}
Output: 
2
Explanation: 
After performing two operations:
Modified array: {3, 3, 11, 7} 
Now, Bitwise AND of all the elements
is 3 & 3 & 11 & 7 = 3 
```

**Example 2:**

```
Input:
N = 3, X = 1
A[] = {2, 2, 2}
Output: 
0
```

**Your Task:**\
You don't need to read input or print anything. Your task is to complete the function **count( )** which takes **N**, **A\[ ]** and **X** as input parameters and returns the minimum number of operations required.

**Expected Time Complexity:** O(N \* Log(max(A\[ ])))\
**Expected Auxiliary Space:** O(1)

**Constraints:**\
1 ≤ N ≤ 10^5\
1 ≤ A\[i] ≤ 10^9\
1 ≤ X ≤ 10^9

### Solution

Algorithm:

Initially lets assume we need to change all the elements, so ans = n

For each bit on X we examine the corresponding bits of all elements

case 1: If bit is set on X, and not on element Then, we need to change this element and mark it as changed. If this element is not marked as change already, increment the change counter (temp)

case2: If bit is not set on X, we calculate how many elements have this bet unset (cnt) Then, we try to calculate ans = min(ans, temp + cnt) Note: we update ans only when bit on X is not set, that way we will get strictly higher value than X.

```cpp
class Solution {
    public:
    int count(int n, vector<int> A, int X)
    {
        int ans = n, temp = 0, vis[n] = {0};
        
        for(int i = 30; i >= 0; i--)
        {
            cout << " i  = " << i << endl;
            int cnt = 0;
            for(int j = 0; j < n; j++)
            {
                cout << "   j = " << j << endl;
                if(vis[j] == 0 && ((X >> i) & 1) && !((A[j] >> i) & 1))
                {
                    temp++;
                    vis[j] = 1;
                    cout << " temp increased to " << temp << " visited set for " << j << endl;
                }
                if(!((A[j] >> i) & 1) && vis[j] == 0)
                {
                    cout << " cnt increased to " << cnt << endl;
                    cnt++;
                }
            }
            if(!((X >> i) & 1))
            {
                ans = min(ans, temp + cnt);
                cout << " Ans changed to " << ans << endl;
            }
        }
        return ans;
    }
};
```
