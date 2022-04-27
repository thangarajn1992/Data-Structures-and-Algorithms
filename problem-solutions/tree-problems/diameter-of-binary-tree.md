# Diameter of Binary Tree

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/diameter-of-binary-tree/1#)

### Companies

* [Google](../../company-based-lists/google.md)
* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given a Binary Tree, **find diameter of it**.The diameter of a tree is the number of nodes on the longest path between two end nodes in the tree. The diagram below shows two trees each with diameter nine, the leaves that form the ends of a longest path are shaded (note that there is more than one path in each tree of length nine, but no path longer than nine nodes).

![](https://contribute.geeksforgeeks.org/wp-content/uploads/diameter.jpg)

**Example 1:**

```
Input:
       1
     /  \
    2    3
Output: 3
```

**Example 2:**

```
Input:
         10
        /   \
      20    30
    /   \ 
   40   60
Output: 4
```

**Expected Time Complexity:** O(N).\
**Expected Auxiliary Space:** O(Height of the Tree).

**Constraints:**\
&#x20;1 <= Number of nodes <= 10000\
&#x20;1 <= Data of a node <= 1000

### Solution

```cpp
class Solution {
  public:
    int dia = 0;
    int diameter(Node* root) {
        height(root);
        return dia;
    }
    int height(Node* root)
    {
        int left = (root->left) ? height(root->left) : 0;
        int right = (root->right) ? height(root->right) : 0;
        dia = max(dia, left+right+1);
        return max(left, right)+1;
    }
};
```
