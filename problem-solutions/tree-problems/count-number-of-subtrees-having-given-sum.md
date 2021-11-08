# Count Number of SubTrees having given Sum

### Sources

* [GeeksForGeeks](https://practice.geeksforgeeks.org/problems/count-number-of-subtrees-having-given-sum/1#)

### Companies

* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given a binary tree and an integer **X**. Your task is to complete the function **countSubtreesWithSumX()** that returns the count of the number of subtress having total node’s data sum equal to the value **X**.\
**Example:** For the tree given below:           &#x20;

&#x20;             5\
&#x20;           /    \\\
&#x20;       \-10     3\
&#x20;       /    \    /  \\\
&#x20;     9     8  -4 7

Subtree with sum 7:\
&#x20;            \-10\
&#x20;           /      \\\
&#x20;         9        8

and one node 7.

**Example 1:**

```
Input:
       5
    /    \
  -10     3
 /   \   /  \
 9   8 -4    7
X = 7
Output: 2
Explanation: Subtrees with sum 7 are
[9, 8, -10] and [7] (refer the example
in the problem description).
```

**Example 2:**

```
Input:
    1
  /  \
 2    3
X = 5
Output: 0
Explanation: No subtree has sum equal
to 5.
```

**Your Task:**\
You don't need to read input or print anything. Your task is to complete the function **countSubtreesWithSumX**() which takes the root node and an integer X as inputs and returns the number of subtrees of the given Binary Tree having sum exactly equal to X.

**Expected Time Complexity: **O(N).\
**Expected Auxiliary Space: **O(Height of the Tree).

**Constraints:**\
1 <= N <= 10^3\
\-10^3 <= Node Value <= 10^3

### Solution

```cpp
int subtreesWithSumXUtil(Node* root, int X, int &count)
{
    if(root == nullptr)
        return 0;
    
    int leftsum = subtreesWithSumXUtil(root->left, X, count);
    int rightsum = subtreesWithSumXUtil(root->right, X, count);
    
    int sum = leftsum + rightsum + root->data;
    if(sum == X)
        count++;
    
    return sum; 
}

int countSubtreesWithSumX(Node* root, int X)
{
    int count = 0;
    subtreesWithSumXUtil(root, X, count);
    return count;
}
```
