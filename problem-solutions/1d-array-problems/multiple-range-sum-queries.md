# Multiple Range Sum Queries

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/sum-of-query-ii5310/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)

### Problem Statement

You are given an array **arr\[\]** of **n** integers and **q** queries in an array **queries\[\]** of length **2\*q** containing **l**, **r** pair for all q queries. You need to compute the following sum over q queries.

![](https://latex.codecogs.com/gif.latex?\sum_{i=l}^{r}arr[i])

Array is 1-Indexed.

**Example 1:**

```text
Input: n = 4
arr = {1, 2, 3, 4}
q = 2
queries = {1, 4, 2, 3}
Output: 10 5
Explaination: In the first query we need sum 
from 1 to 4 which is 1+2+3+4 = 10. In the 
second query we need sum from 2 to 3 which is 
2 + 3 = 5.
```

**Your Task:**  
 You do not need to read input or print anything. Your task is to complete the function **querySum\(\)** which takes n, arr, q and queries as input parameters and returns the answer for all the queries.

**Expected Time Complexity:** O\(n+q\)  
 **Expected Auxiliary Space:** O\(n\)

**Constraints:**  
 1 ≤ n, q ≤ 1000  
 1 ≤ arr\[i\] ≤ 10^6  
 1 ≤ l ≤ r ≤ n

### Solution

```cpp
class Solution{
public:
    vector<int> querySum(int n, int arr[], int q, int queries[])
    {
        vector<int> prefixSum(n+1, 0);
        for(int i = 1; i <= n; i++)
            prefixSum[i] = prefixSum[i-1] + arr[i-1];
        
        vector<int> queryResults;
        int qSize = q*2;
        for(int i = 0; i < qSize; i+=2)
            queryResults.push_back(prefixSum[queries[i+1]] - prefixSum[queries[i]-1]);
        
        return queryResults;
    }
};
```

