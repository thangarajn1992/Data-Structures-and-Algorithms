# Select maximum number of elements within given sum

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/maximize-toys0331/1#)

### Companies

* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given an array **arr\[ \]** of length **N** consisting cost of **N** toys and an integer **K** depicting the amount with you. Your task is to find maximum number of toys you can buy with **K** amount. 

**Example 1:**

```text
Input: 
N = 7 
K = 50
arr[] = {1, 12, 5, 111, 200, 1000, 10}
Output: 4
Explaination: The costs of the toys 
you can buy are 1, 12, 5 and 10.
```

**Example 2:**

```text
Input: 
N = 3 
K = 100
arr[] = {20, 30, 50}
Output: 3
Explaination: You can buy all toys.
```

**Expected Time Complexity:** O\(N \* Log\(N\)\)  
**Expected Auxiliary Space:** O\(1\)

**Constraints:**  
 1 ≤ N ≤ 10^5  
 1 ≤ K, arr\[i\] ≤ 10^9

### Solution

```cpp
class Solution{
public:
    int toyCount(int N, int K, vector<int> arr)
    {
        sort(arr.begin(), arr.end());
        int toyNum, curSum = 0;
        for(toyNum = 0; toyNum < N; toyNum++)
            if((curSum += arr[toyNum])  > K)
                break;
        return toyNum;
    }
};
```

