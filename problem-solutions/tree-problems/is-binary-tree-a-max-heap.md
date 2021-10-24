# Is Binary Tree a Max Heap

### Sources

* [GeeksForGeeks](https://practice.geeksforgeeks.org/problems/is-binary-tree-heap/1#)

### Companies

### Problem Statement

Given a binary tree you need to check if it follows max heap property or not.\
\
**Input:**\
The task is to complete the method which takes one argument, root of Binary Tree. The struct Node has a data part which stores the data, pointer to left child and pointer to right child.There are multiple test cases. For each test case, this method will be called individually.\
\
**Output:**\
The function should return true if property holds else false.\
&#x20;

**Example 1:**

```
Input:
      5
    /  \
   2    3
Output: 1
```

**Example 2:**

```
Input:
       10
     /   \
    20   30 
  /   \
 40   60
Output: 0
```

**Constraints:**\
1 ≤ Number of nodes ≤ 100\
1 ≤ Data of a node ≤

### Solution

```cpp
class Solution {
  public:
    bool isHeap(struct Node* tree) {
        // These two are used in isCompleteUtil()
        unsigned int node_count = countNodes(tree);
        unsigned int index = 0;
  
        if (isCompleteUtil(tree, index, node_count) && isHeapUtil(tree))
            return true;
        return false;
    }
    
    /* This function counts the number of nodes in a binary tree */
    unsigned int countNodes(struct Node* root)
    {
        if (root == NULL)
            return 0;
        return (1 + countNodes(root->left) + countNodes(root->right));
    }
  
    /* This function checks if the binary tree is complete or not */
    bool isCompleteUtil(struct Node* root, unsigned int index,
                        unsigned int number_nodes)
    {
        // An empty tree is complete
        if (root == NULL)
            return true;
  
        // If index assigned to current node is more than 
        // number of nodes in tree, then tree is not complete
        if (index >= number_nodes)
            return false;
  
        // Recur for left and right subtrees
        return (isCompleteUtil(root->left, 2*index + 1, number_nodes) &&
                isCompleteUtil(root->right, 2*index + 2, number_nodes));
    }
 
    // This Function checks the heap property in the tree.
    bool isHeapUtil(struct Node* root)
    {
        //  Base case : single node satisfies property
        if (root->left == NULL && root->right == NULL)
            return true;
  
        //  node will be in second last level
        if (root->right == NULL)
        {
            // check heap property at Node No recursive call ,
            // because no need to check last level
            return (root->data >= root->left->data);
        }
        else
        {
            //  Check heap property at Node and Recursive check heap
            // property at left and right subtree
            if (root->data >= root->left->data &&
                root->data >= root->right->data)
                return ((isHeapUtil(root->left)) && (isHeapUtil(root->right)));
            else
                return (false);
        }
    }
};
```

