# Maximum path sum from any node

### Source

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/maximum-path-sum-from-any-node/1#)

### Problem Statement

Given a binary tree, the task is to find the maximum path sum. The path may start and end at any node in the tree.

**Example 1:**

```text
Input:
     10
    /  \
   2   -25
  / \  /  \
 20 1  3  4
Output: 32
Explanation: Path in the given tree goes
like 10 , 2 , 20 which gives the max
sum as 32.
```

**Example 2:**

```text
Input:
     10
   /    \
  2      5
          \
          -2
Output: 17
Explanation: Path in the given tree goes
like 2 , 10 , 5 which gives the max sum
as 17.
```

**Expected Time Complexity:** O\(N\).  
**Expected Auxiliary Space:** O\(Height of the Tree\).

**Constraints:**  
 1 ≤ Number of nodes ≤ 10^3  
 1 ≤ \|Data on node\| ≤ 10^4

### Solution

```cpp
class Solution {
  public:
    int maxSum = INT_MIN;
    int findMaxSum(Node* root)
    {
        findMaxUtil(root);
        return maxSum;
    }
    
    int findMaxUtil(Node *root)
    {
        if(!root)
            return 0;
    
        
        int leftSum = findMaxUtil(root->left);
        int rightSum = findMaxUtil(root->right);
        
        int childMax = max(leftSum, rightSum);
        
        int currSum = max(root->data, 
                           max(root->data + leftSum, 
                               max(root->data + rightSum,
                                   root->data + leftSum + rightSum)));
        
        if(currSum > maxSum)
            maxSum = currSum;
        
        return max(root->data, root->data + childMax);
    }
};
```

