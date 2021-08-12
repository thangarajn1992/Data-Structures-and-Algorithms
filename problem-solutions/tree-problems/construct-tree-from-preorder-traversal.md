# Construct Tree from Preorder Traversal

### Source

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/construct-tree-from-preorder-traversal/1#)

### Problem Statement

Construct a binary tree of size **N** using two given arrays **pre\[\]** and **preLN\[\]**. Array **pre\[\]** represents preorder traversal of a binary tree. Array **preLN\[\]** has only two possible values ‘**L**’ and ‘**N**’. The value ‘**L**’ in **preLN\[\]** indicates that the corresponding node in Binary Tree is a leaf node and value ‘N’ indicates that the corresponding node is a non-leaf node.  
 **Note:** Every node in the binary tree has either 0 or 2 children.

**Example 1:**

```text
Input :      
N = 5
pre[] = {10, 30, 20, 5, 15}
preLN[] = {N, N, L, L, L}

Output:
          10
        /    \
      30      15
     /  \     
   20    5   
```

**Expected Time Complexity:** O\(N\)  
**Expected Auxiliary Space:** O\(N\)  
**Constraints:**  
 1 ≤ N ≤ 10^4  
 1 ≤ pre\[i\] ≤ 10^7  
 preLN\[i\]: {'N', 'L'}

### Solution

#### Iterative Approach

```cpp
struct Node *constructTree(int n, int pre[], char preLN[])
{
    stack<struct Node *> s;
    struct Node *tree = new struct Node(pre[0]);
    s.push(tree);
    
    for(int i = 1; i < n; i++)
    {
        struct Node *cur = s.top();
        if(preLN[i] == 'N')
        {
            if(cur->left == nullptr)
            {
                cur->left = new struct Node(pre[i]);
                s.push(cur->left);
            }
            else
            {
                cur->right = new struct Node(pre[i]);
                s.pop();
                s.push(cur->right);
            }
        }
        else
        {
            if(cur->left == nullptr)
                cur->left = new struct Node(pre[i]);
            else
            {
                cur->right = new struct Node(pre[i]);
                s.pop();
            }
        }
    }
    return tree;
}
```

