# Maximum Path Sum between 2 Leaf Nodes

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/maximum-path-sum/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Facebook](../../company-based-lists/facebook.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given a binary tree in which each node element contains a number. Find the maximum possible path sum from one leaf node to another leaf node.

**Note:** Here Leaf node is a node which is connected to exactly one different node.

\
 **Example 1:**

```
Input:      
           3                               
         /    \                          
       4       5                     
      /  \      
    -10   4                          
Output: 16
Explanation:
Maximum Sum lies between leaf node 4 and 5.
4 + 4 + 3 + 5 = 16.
```

**Example 2:**

```
Input:    
            -15                               
         /      \                          
        5         6                      
      /  \       / \
    -8    1     3   9
   /  \              \
  2   -3              0
                     / \
                    4  -1
                       /
                     10  
Output:  27
Explanation:
The maximum possible sum from one leaf node 
to another is (3 + 6 + 9 + 0 + -1 + 10 = 27)
```

**Expected Time Complexity:** O(N)\
**Expected Auxiliary Space:** O(Height of Tree)

\
 **Constraints:**\
 2  ≤  Number of nodes  ≤  10^4\
 \-10^3  ≤ Value of each node ≤ 10^3

### Solution

```cpp
class Solution {
public:
    int maxsum;
    int maxPathSum(Node* root)
    {
        maxsum = INT_MIN;
        int val = util(root);
        // maxsum will be INT_MIN if it is one-sided tree
        return (maxsum != INT_MIN) ? maxsum : val;
    }
    int util(Node* root)
    {
        if(root->left)
        {
            int left = util(root->left);
            if(root->right)
            {
                int right = util(root->right);
                // update maxsum only on nodes which has both right & left nodes
                maxsum = max(maxsum, left+right+root->data);
                return root->data+max(right,left);
            }
            return root->data+left;
        }
        else
        {
            if(root->right)
                return root->data + util(root->right);
            else
                return root->data;
        }
    }
};
```
