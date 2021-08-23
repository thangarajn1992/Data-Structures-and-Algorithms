# Two Nodes sum up to target

### Sources

* [Leetcode 653](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/)

### Companies

### Problem Statement

Given the `root` of a Binary Search Tree and a target number `k`, return _`true` if there exist two elements in the BST such that their sum is equal to the given target_.

**Example 1:** ![](https://assets.leetcode.com/uploads/2020/09/21/sum_tree_1.jpg)

```text
Input: root = [5,3,6,2,4,null,7], k = 9
Output: true
```

**Example 2:** ![](https://assets.leetcode.com/uploads/2020/09/21/sum_tree_2.jpg)

```text
Input: root = [5,3,6,2,4,null,7], k = 28
Output: false
```

**Example 3:**

```text
Input: root = [2,1,3], k = 4
Output: true
```

**Example 4:**

```text
Input: root = [2,1,3], k = 1
Output: false
```

**Example 5:**

```text
Input: root = [2,1,3], k = 3
Output: true
```

**Constraints:**

* The number of nodes in the tree is in the range `[1, 10^4]`.
* `-10^4 <= Node.val <= 10^4`
* `root` is guaranteed to be a **valid** binary search tree.
* `-10^5 <= k <= 10^5`

### Solution

#### Hash-Map + BFS using queue

```cpp
class Solution {
public:
    bool findTarget(TreeNode* root, int k) {
        set<int> seen;
        queue<TreeNode*> q;
        q.push(root);
        
        while(q.empty() == false)
        {
            for(int i = q.size()-1; i >= 0; i--)
            {
                TreeNode * curr = q.front(); q.pop();
                if(seen.count(k - curr->val))
                    return true;
                seen.insert(curr->val);
                if(curr->left) q.push(curr->left);
                if(curr->right) q.push(curr->right);
            }
        }
        return false;
    }
};
```

