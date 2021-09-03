# Generate all possible structurally unique BSTs with n nodes with unique value from 1 to n

### Sources

* [Leetcode 95](https://leetcode.com/problems/unique-binary-search-trees-ii/)

### Companies

### Problem Statement

Given an integer `n`, return _all the structurally unique **BST'**s \(binary search trees\), which has exactly_ `n` _nodes of unique values from_ `1` _to_ `n`. Return the answer in **any order**.

**Example 1:** 

![](https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg)

```text
Input: n = 3
Output: [[1,null,2,null,3],[1,null,3,2],[2,1,3],[3,1,null,null,2],[3,2,null,1]]
```

**Example 2:**

```text
Input: n = 1
Output: [[1]]
```

**Constraints:**

* `1 <= n <= 8`

### Solution

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    map<int, vector<TreeNode*>> preCalc;
    vector<TreeNode*> generateTrees(int n) {
        return generateTreesUtil(1, n);
    }
    vector<TreeNode*> generateTreesUtil(int start, int end)
    {
        if(start > end)
            return {nullptr};
            
        int x = start*10 + end;
        
        if(preCalc.find(x) != preCalc.end())
            return preCalc[x];
        vector<TreeNode*> result;
        
        //Keep each element from start to end as root and generate sub-trees
        for(int root = start; root <= end; root++)
        {
            vector<TreeNode*> left = generateTreesUtil(start, root-1);
            vector<TreeNode*> right = generateTreesUtil(root+1, end);
            
            for(TreeNode* l : left)
                for(TreeNode* r : right)
                    result.push_back(new TreeNode(root, l, r));
        }
        preCalc[x] = result;
        return result;
    }
};
```

