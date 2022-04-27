# Print BST elements in given range

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/print-bst-elements-in-given-range/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Flipkart](../../company-based-lists/flipkart.md)

### Problem Statement

Given a Binary Search Tree **** and a range **\[low, high]**. Find all the numbers in the BST that lie in the given range. **Note:** Element greater than or equal to root go to the right side. Complete the function **printNearNodes()** which takes the root Node of the BST and the range elements low and high as inputs and returns an array that contains the BST elements in the given range low to high (inclusive) in **non-decreasing** order.

**Example 1:**

```
Input:
       17
     /    \
    4     18
  /   \
 2     9 
l = 4, h = 24
Output: 4 9 17 18 
```

**Example 2:**

```
Input:
       16
     /    \
    7     20
  /   \
 1    10
l = 13, h = 23
Output: 16 20 
```

**Expected Time Complexity:** O(N).\
**Expected Auxiliary Space:** O(Height of the BST).

**Constraints:**\
&#x20;1 ≤ Number of nodes ≤ 10^4\
&#x20;1 ≤ l ≤ h ≤ 10^5

### Solution

```cpp
class Solution {
  public:
    vector<int> printNearNodes(Node *root, int low, int high) {
        vector<int> nodesInRange;
        inorder(root, low, high, nodesInRange);
        return nodesInRange;
    }
    
    void inorder(Node *root, int low, int high, vector<int> &nodesInRange)
    {
        if(root == nullptr)
            return;
        
        if(root->data >= low)
        {
            inorder(root->left, low, high, nodesInRange);
            if(root->data <= high)
                nodesInRange.push_back(root->data);
        }
        
        if(root->data <= high)
            inorder(root->right, low, high, nodesInRange);
    }
};
```

