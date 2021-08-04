# Root to Leaf Paths with specific sum

### Source

* [Leetcode 113](https://leetcode.com/problems/path-sum-ii/)

### Problem Statement

Given the `root` of a binary tree and an integer `targetSum`, return all **root-to-leaf** paths where each path's sum equals `targetSum`.

A **leaf** is a node with no children.

**Example 1:** ![](https://assets.leetcode.com/uploads/2021/01/18/pathsumii1.jpg)

```text
Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
Output: [[5,4,11,2],[5,8,4,5]]
```

**Example 2:** ![](https://assets.leetcode.com/uploads/2021/01/18/pathsum2.jpg)

```text
Input: root = [1,2,3], targetSum = 5
Output: []
```

**Example 3:**

```text
Input: root = [1,2], targetSum = 0
Output: []
```

**Constraints:**

* The number of nodes in the tree is in the range `[0, 5000]`.
* `-1000 <= Node.val <= 1000`
* `-1000 <= targetSum <= 1000`

### Solution

```cpp
class Solution {
public:
    vector<vector<int>> paths_with_target_sum;
    vector<int> cur_path;
    vector<vector<int>> pathSum(TreeNode* root, int targetSum) {         
        pathSumUtil(root, targetSum);
        return paths_with_target_sum;
    }
    void pathSumUtil(TreeNode* root, int targetSum)
    {
        if(!root)
            return;
        
        cur_path.push_back(root->val);
       
        if(root->left == nullptr && root->right == nullptr && root->val == targetSum)
        {
            paths_with_target_sum.push_back(cur_path);
            cur_path.pop_back();
            return;
        }
        pathSumUtil(root->left, targetSum - root->val);
        
        pathSumUtil(root->right, targetSum - root->val);
        cur_path.pop_back();
        
    }
};
```

