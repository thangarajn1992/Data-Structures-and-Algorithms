# Subset Sums

### Source

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/subset-sums2234/1#)

### Problem Statement

Given a list **arr** of **N** integers, print sums of all subsets in it. Output should be printed in increasing order of sums.

**Example 1:**

```text
Input:
N = 2
arr[] = {2, 3}
Output:
0 2 3 5
Explanation:
When no elements is taken then Sum = 0.
When only 2 is taken then Sum = 2.
When only 3 is taken then Sum = 3.
When element 2 and 3 are taken then 
Sum = 2+3 = 5.
```

**Example 2:**

```text
Input:
N = 3
arr = {5, 2, 1}
Output:
0 1 2 3 5 6 7 8
```

**Your Task:**    
 You don't need to read input or print anything. Your task is to complete the function **subsetSums**\(\) which takes a list/vector and an integer **N** as an input parameter and return the list/vector of all the subset sums in increasing order.

**Expected Time Complexity:** O\(2^N\)  
 **Expected Auxiliary Space:** O\(2^N\)

**Constraints:**  
 1 &lt;= N &lt;= 15  
 0 &lt;= arr\[i\] &lt;= 10000

### Solution

#### Iterative Approach

```cpp
class Solution
{
public:
    vector<int> subsetSums(vector<int> arr, int N)
    {
        vector<int> subsetSum;
        int totalSubsets = 1 << N;
        for(int subsetNum = 0; subsetNum < totalSubsets; subsetNum++)
        {
            int sum = 0;
            for(int index = 0; index < N; index++)
            {
                if(subsetNum & (1 << index))
                    sum += arr[index];
            }
            subsetSum.push_back(sum);
        }
        sort(subsetSum.begin(), subsetSum.end());
        return subsetSum;    }
};
```

#### Recursive Approach

```cpp
class Solution
{
public:
    vector<int> subsetSum;
    vector<int> subsetSums(vector<int> arr, int N)
    {
        findSubsetsUtil(arr, 0, N-1, 0);
        sort(subsetSum.begin(), subsetSum.end());
        return subsetSum;
    }
    void findSubsetsUtil(vector<int>&arr, int index, int size, int sum)
    {
        if(index > size)
        {
            subsetSum.push_back(sum);
            return;
        }
        
        // subset with this element
        findSubsetsUtil(arr, index+1, size, sum + arr[left]);
        
        // subset without this element
        findSubsetsUtil(arr, index+1, size, sum);
    }
};
```

