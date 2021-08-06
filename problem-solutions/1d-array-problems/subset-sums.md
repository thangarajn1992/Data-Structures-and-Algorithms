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
        // Write Your Code here
        vector<int> sub_sum;
        int total = 1 << N;
        for(int i = 0; i < total; i++)
        {
            int sum = 0;
            for(int j = 0; j < N; j++)
            {
                if(i & (1 << j))
                    sum += arr[j];
            }
            sub_sum.push_back(sum);
        }
        sort(sub_sum.begin(), sub_sum.end());
        return sub_sum;
    }
};
```

#### Recursive Approach

```cpp
class Solution
{
public:
    vector<int> sub_sum;
    vector<int> subsetSums(vector<int> arr, int N)
    {
        subset_recur(arr, 0, N-1, 0);
        sort(sub_sum.begin(), sub_sum.end());
        return sub_sum;
    }
    void subset_recur(vector<int>&arr, int left, int right, int sum)
    {
        if(left > right)
        {
            sub_sum.push_back(sum);
            return;
        }
        
        // subset with this element
        subset_recur(arr, left+1, right, sum + arr[left]);
        
        // subset without this element
        subset_recur(arr, left+1, right, sum);
    }
};
```

