# Validate Binary Search Tree

### Sources

* [Leetcode 98](https://leetcode.com/problems/validate-binary-search-tree/)
* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/check-for-bst/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Flipkart](../../company-based-lists/flipkart.md)
* [Walmart](../../company-based-lists/walmart.md)
* [Samsung](../../company-based-lists/samsung.md)
* [Adobe](../../company-based-lists/adobe.md)

### Problem Statement

Given the `root` of a binary tree, _determine if it is a valid binary search tree \(BST\)_.

A **valid Binary Search Tree** is defined as follows:

* The left sub-tree of a node contains only nodes with keys **less than** the node's key.
* The right sub-tree of a node contains only nodes with keys **greater than** the node's key.
* Both the left and right sub-trees must also be binary search trees.

**Example 1:** 

![](https://assets.leetcode.com/uploads/2020/12/01/tree1.jpg)

```text
Input: root = [2,1,3]
Output: true
```

**Example 2:** 

![](https://assets.leetcode.com/uploads/2020/12/01/tree2.jpg)

```text
Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
```

**Constraints:**

* The number of nodes in the tree is in the range `[1, 10^4]`.
* `-2^31 <= Node.val <= 2^31 - 1`

### Solution

```cpp
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        return isValidBSTUtil(root, LONG_MIN, LONG_MAX);
    }
    
    bool isValidBSTUtil(TreeNode* root, long min, long max)
    {
        if(root == nullptr)
            return true;
        
        if(root->val <= min || root->val >= max)
            return false;
        
        return isValidBSTUtil(root->left, min, root->val) &&
                isValidBSTUtil(root->right, root->val, max);

    }
};
```

