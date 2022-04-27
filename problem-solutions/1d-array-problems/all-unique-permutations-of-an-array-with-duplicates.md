# All Unique Permutations of an array with duplicates

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/all-unique-permutations-of-an-array/1#)
* [Leetcode 47](https://leetcode.com/problems/permutations-ii/)

### Companies

* [Google](../../company-based-lists/google.md)

### Problem Statement

Given an array **arr\[]** of length **n.** Find all possible unique permutations of the array.

\
**Example 1:**

```
Input: 
n = 3
arr[] = {1, 2, 1}
Output: 
1 1 2
1 2 1
2 1 1
Explanation:
These are the only possible unique permutations
for the given array.
```

**Example 2:**

```
Input: 
n = 2
arr[] = {4, 5}
Output: 
4 5
5 4
```

\
**Your Task:**\
You don't need to read input or print anything. You only need to complete the function **uniquePerms()** that takes an integer n, and an array arr of size n as input and returns a sorted list of lists containing all unique permutations of the array.

\
**Expected Time Complexity:**  O(n\*n!)\
**Expected Auxilliary Space:** O(n\*n!)\
&#x20;

**Constraints:**\
1 ≤ n ≤ 10\
1 ≤ arr\[i] ≤ 10

### Solution

```cpp
class Solution {
  public:
    vector<vector<int>> uniquePerms(vector<int> num ,int n) {
        sort(num.begin(), num.end());
        vector<vector<int>> res;
        recursion(num, 0, res);
        return res;
    }
    void recursion(vector<int> num, int i, vector<vector<int>> &res) {
        if (i == num.size() - 1) {
            res.push_back(num);
            return;
        }
        for (int k = i; k < num.size(); k++) {
            if (i != k && num[i] == num[k]) 
                continue;
            swap(num[i], num[k]);
            recursion(num, i+1, res);
        }
    }
};
```
