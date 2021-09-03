# Number of Structurally unique BSTs with n nodes with unique value from 1 to n

### Sources

* [Leetcode 96](https://leetcode.com/problems/unique-binary-search-trees/)

### Companies

### Problem Statement

Given an integer `n`, return _the number of structurally unique **BST'**s \(binary search trees\) which has exactly_ `n` _nodes of unique values from_ `1` _to_ `n`.

**Example 1:** 

![](https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg)

```text
Input: n = 3
Output: 5
```

**Example 2:**

```text
Input: n = 1
Output: 1
```

**Constraints:**

* `1 <= n <= 19`

### Solution

#### Dynamic Programming Approach

```cpp
class Solution {
public:
    int numTrees(int n) {
        vector<int> treeCount(n+1, 0);
        treeCount[0] = 1;  // root null case  
        treeCount[1] = 1; // Single node case
        
        for(int i = 2; i <= n; i++){
            for(int j = 0; j < i; j++){ // j is no.of nodes in left sub-tree
                treeCount[i] += treeCount[j] * treeCount[i-j-1];
            }
        }
        return treeCount[n];     
    }
};
```

#### Recursive Approach

```cpp
class Solution {
public:
    map<vector<int>, int> preCalc;
    
    int numTrees(int n) {
        return getTreeCount(1, n);
    }
    
    // Returns number of possible trees possible with given range
    int getTreeCount(int start, int end)
    {
        if(start >= end)
            return 1;
        if(preCalc.find({start, end}) != preCalc.end())
            return preCalc[{start,end}];
        
        int treeCount = 0;
         //Keep each element from start to end as root and generate sub-trees
        for(int root = start; root <= end; root++)
        {
            int left = getTreeCount(start, root-1);
            int right = getTreeCount(root+1, end);
            
            treeCount += left*right;
        }   
        preCalc[{start,end}] = treeCount;
        return treeCount;
    }
};
```

