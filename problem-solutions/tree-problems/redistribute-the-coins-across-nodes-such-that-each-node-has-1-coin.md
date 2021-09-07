# Redistribute the coins across Nodes such that each node has 1 coin

### Sources

* [Leetcode 979](https://leetcode.com/problems/distribute-coins-in-binary-tree/)

### Companies

### Problem Statement

You are given the `root` of a binary tree with `n` nodes where each `node` in the tree has `node.val` coins. There are `n` coins in total throughout the whole tree.

In one move, we may choose two adjacent nodes and move one coin from one node to another. A move may be from parent to child, or from child to parent.

Return _the **minimum** number of moves required to make every node have **exactly** one coin_.

**Example 1:** ![](https://assets.leetcode.com/uploads/2019/01/18/tree1.png)

```text
Input: root = [3,0,0]
Output: 2
Explanation: From the root of the tree, we move one coin to its left child, and one coin to its right child.
```

**Example 2:** ![](https://assets.leetcode.com/uploads/2019/01/18/tree2.png)

```text
Input: root = [0,3,0]
Output: 3
Explanation: From the left child of the root, we move two coins to the root [taking two moves]. Then, we move one coin from the root of the tree to the right child.
```

**Example 3:** ![](https://assets.leetcode.com/uploads/2019/01/18/tree3.png)

```text
Input: root = [1,0,2]
Output: 2
```

**Example 4:** ![](https://assets.leetcode.com/uploads/2019/01/18/tree4.png)

```text
Input: root = [1,0,0,null,3]
Output: 4
```

**Constraints:**

* The number of nodes in the tree is `n`.
* `1 <= n <= 100`
* `0 <= Node.val <= n`
* The sum of all `Node.val` is `n`.

### Algorithm

* Root asks the left subtree, how much do you need or you've got extra? I'll give that/take it away to/from you via our direct edge, and pass it to right child, and if something remains, I'll take it.
* Same question is asked to the right child.
* Answer will be the sum of values\(absolute\) returned after the asked questions from the left\(Left\) and right\(Right\).
* But what should the root return to its parent? It will return that how much does "his tree" need/has extra. That will be the signed sum of its Left+Right \(question's answer\) + same question asked to current root node.

### Solution

```cpp
class Solution {
public:
    int movesRequired = 0;
    int distributeCoins(TreeNode* root) {
        CoinsNeededorExtra(root);
        return movesRequired;
    }
    
    // Updates the moves needed inside its sub-tree to distribute coins
    // After performing those moves, it returns number of coins 
    //it still needs or has extra to its caller.
    int CoinsNeededorExtra(TreeNode* root)
    {
        if(root == nullptr)
            return 0;
        
        int leftCoins = CoinsNeededorExtra(root->left);
        int rightCoins = CoinsNeededorExtra(root->right);
        
        // moves require to distribute coins within its subtree
        movesRequired += abs(leftCoins) + abs(rightCoins);
        
        //After those moves, this node returns the extra or needed coins to its parent
        return leftCoins + rightCoins + (root->val - 1);  // -1 is for this node's coin
    }
};
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
```

