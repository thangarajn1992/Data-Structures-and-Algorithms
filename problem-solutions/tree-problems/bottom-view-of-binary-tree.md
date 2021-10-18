# Bottom View of Binary Tree

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/bottom-view-of-binary-tree/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Flipkart](../../company-based-lists/flipkart.md)
* [Walmart](../../company-based-lists/walmart.md)

### Problem Statement

Given a binary tree, print the bottom view from left to right. A node is included in bottom view if it can be seen when we look at the tree from bottom.

                      20\
                     /    \\\
                   8       22\
                 /   \        \\\
               5      3       25\
                     /   \      \
                   10    14

For the above tree, the bottom view is 5 10 3 14 25. If there are **multiple** bottom-most nodes for a horizontal distance from root, then print the later one in level traversal. For example, in the below diagram, 3 and 4 are both the bottom most nodes at horizontal distance 0, we need to print 4.

                      20\
                     /    \\\
                   8       22\
                 /   \     /   \\\
               5      3 4     25\
                      /    \      \
                  10       14

For the above tree the output should be 5 10 4 14 25.\
  

**Example 1:**

```
Input:
       1
     /   \
    3     2
Output: 3 1 2
Explanation:
First case represents a tree with 3 nodes
and 2 edges where root is 1, left child of
1 is 3 and right child of 1 is 2.

Thus nodes of the binary tree will be
printed as such 3 1 2.
```

![](<../../.gitbook/assets/image (27).png>)

**Example 2:**

```
Input:
         10
       /    \
      20    30
     /  \
    40   60
Output: 40 20 60 30
```

**Expected Time Complexity: **O(N).\
**Expected Auxiliary Space: **O(N).

**Constraints:**\
 1 <= Number of nodes <= 10^5\
 1 <= Data of a node <= 10**^**5

### Solution

#### Use Queue for BFS and keep updating map for each hd

```cpp
struct node_with_hd{
    Node *node;
    int hd; // horizontal_distance
    node_with_hd(Node *root, int my_hd){
        this->node = root;
        this->hd = my_hd;
    }
};
class Solution {
  public:
    map<int,int> horizontalDistance;
    vector <int> bottomView(Node *root) {
        // DO BFS and update the map accordingly with latest values for each HD
        // Queue has treenode and its hd value
        queue<node_with_hd> q;
        node_with_hd qnode(root, 0);
        q.push(qnode);
        while(q.empty() == false)
        {
            int size = q.size();
            for(int i = size-1; i >= 0; i--)
            {
                node_with_hd cur = q.front(); q.pop();
                horizontalDistance[cur.hd] = cur.node->data;
                if(cur.node->left != nullptr)
                {
                    node_with_hd left(cur.node->left, cur.hd-1);
                    q.push(left);
                }
                if(cur.node->right != nullptr)
                {
                    node_with_hd right(cur.node->right, cur.hd+1);
                    q.push(right);
                }
            }
        }
        vector<int> bottomViewResult;
        for(auto item = horizontalDistance.begin(); item != horizontalDistance.end(); item++)
            bottomViewResult.push_back(item->second);
        
        return bottomViewResult;
    }
};
```
