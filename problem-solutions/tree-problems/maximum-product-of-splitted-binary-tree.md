# Maximum Product of Splitted Binary Tree

### Source

* [Leetcode 1339](https://leetcode.com/problems/maximum-product-of-splitted-binary-tree/)

### Problem Statement

Given the `root` of a binary tree, split the binary tree into two sub-trees by removing one edge such that the product of the sums of the sub-trees is maximized.

Return _the maximum product of the sums of the two sub-trees_. Since the answer may be too large, return it **modulo** `10^9 + 7`.

**Note** that you need to maximize the answer before taking the mod and not after taking it.

**Example 1:** 

![](https://assets.leetcode.com/uploads/2020/01/21/sample_1_1699.png)

```text
Input: root = [1,2,3,4,5,6]
Output: 110
Explanation: 
Remove the red edge and get 2 binary trees with sum 11 and 10. Their product is 110 (11*10)
```

**Example 2:** 

![](https://assets.leetcode.com/uploads/2020/01/21/sample_2_1699.png)

```text
Input: root = [1,null,2,3,4,null,null,5,6]
Output: 90
Explanation: Remove the red edge and get 2 binary trees with sum 15 and 6.Their product is 90 (15*6)
```

**Example 3:**

```text
Input: root = [2,3,9,10,7,8,6,5,4,11,1]
Output: 1025
```

**Example 4:**

```text
Input: root = [1,1]
Output: 1
```

**Constraints:**

* The number of nodes in the tree is in the range `[2, 5 * 10^4]`.
* `1 <= Node.val <= 10^4`

### Solution

```cpp
class Solution {
public:
    long long maxPdt = 0, totalSum = 0;
    int maxProduct(TreeNode* root) {
        // Find Total sum of all nodes in the Binary Tree
        totalSum = findTotalSum(root); 
        // DFS in post order to calculate sum of each subtree and its complement
        dfs(root); 
        return maxPdt % int(1e9+7);
    }
    
    int findTotalSum(TreeNode* root)
    {
        if(root != nullptr)
            return root->val + findTotalSum(root->left) + findTotalSum(root->right);
        return 0;
    }
    
    int dfs(TreeNode* root) {
        if (root == nullptr) 
            return 0;
        int currSum = dfs(root->left) + dfs(root->right) + root->val;
        maxPdt = max(maxPdt, (totalSum - currSum) * currSum);
        return currSum;
    }
};
```

