# Top View of Binary Tree

### Sources

* [GeeksForGeeks](https://practice.geeksforgeeks.org/problems/top-view-of-binary-tree/1#)

### Companies

* [Walmart](../../company-based-lists/walmart.md)

### Problem Statement

Given below is a binary tree. The task is to print the top view of binary tree. Top view of a binary tree is the set of nodes visible when the tree is viewed from the top. For the given below tree

&#x20;      1\
&#x20;   /     \\\
&#x20;  2       3\
&#x20; /  \    /   \\\
4    5  6   7

Top view will be: 4 2 1 3 7\
**Note: **Return nodes from **leftmost **node to **rightmost **node.

**Example 1:**

```
Input:
      1
   /    \
  2      3
Output: 2 1 3
```

**Example 2:**

```
Input:
       10
    /      \
  20        30
 /   \    /    \
40   60  90    100
Output: 40 20 10 30 100
```

**Your Task:**\
Since this is a function problem. You don't have to take input. Just complete the function** topView() **that takes **root node **as parameter and returns a list of nodes visible from the top view from left to right.

**Expected Time Complexity: **O(N)\
**Expected Auxiliary Space: **O(N).

**Constraints:**\
1 ≤ N ≤ 10^5\
1 ≤ Node Data ≤ 10^5

### Solution

#### Breadth First Search Approach

```cpp
class Solution
{
    public:
    //Function to return a list of nodes visible from the top view 
    //from left to right in Binary Tree.
    vector<int> topView(Node *root)
    {
        map<int, int> distanceMap;
        
        queue<pair<Node*, int>> q;
        q.push({root, 0});
        distanceMap[0] = root->data;
        
        while(q.empty() == false)
        {
            for(int n = q.size()-1; n >= 0; n--)
            {
                Node *current = q.front().first;
                int distance = q.front().second;
                q.pop();
                if(current->left != nullptr)
                {
                    q.push({current->left, distance-1});
                    if(distanceMap.find(distance-1) == distanceMap.end())
                        distanceMap[distance-1] = current->left->data;
                }
                if(current->right != nullptr)
                {
                    q.push({current->right, distance+1});
                    if(distanceMap.find(distance+1) == distanceMap.end())
                        distanceMap[distance+1] = current->right->data;
                }
            }
        }
        vector<int> binaryTreeTopView;
        for(auto it = distanceMap.begin(); it != distanceMap.end() ; it++)
            binaryTreeTopView.push_back(it->second);
        
        return binaryTreeTopView;    
    }

};
```
