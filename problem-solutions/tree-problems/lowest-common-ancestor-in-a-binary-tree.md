# Lowest Common Ancestor in a Binary Tree

### Sources

* [GeeksForGeeks](https://practice.geeksforgeeks.org/problems/lowest-common-ancestor-in-a-binary-tree/1#)
* [Leetcode 236](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

### Companies

* [Google](../../company-based-lists/google.md)
* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [PayPal](../../company-based-lists/paypal.md)
* [Flipkart](../../company-based-lists/flipkart.md)

### Problem Statement

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest\_common\_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow **a node to be a descendant of itself**).”

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
```

**Example 3:**

```
Input: root = [1,2], p = 1, q = 2
Output: 1
```

&#x20;

**Constraints:**

* The number of nodes in the tree is in the range `[2, 10^5]`.
* `-10^9 <= Node.val <= 10^9`
* All `Node.val` are **unique**.
* `p != q`
* `p` and `q` will exist in the tree.

### Solution

```cpp
class Solution
{
    public:
    //Function to return the lowest common ancestor in a Binary Tree.
    Node* lca(Node* root ,int n1 ,int n2 )
    {
       if(root == nullptr)
            return nullptr;
       
       if(root->data == n1 || root->data == n2)
            return root;
       
       Node* left = lca(root->left, n1, n2);
       Node* right = lca(root->right, n1, n2);
       
       if(left != nullptr && right != nullptr)
           return root;
       
       return left != nullptr ? left : right;
    }
};
```
