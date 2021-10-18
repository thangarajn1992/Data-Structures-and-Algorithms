# Vertical Traversal of Binary Tree

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/print-a-binary-tree-in-vertical-order/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Flipkart](../../company-based-lists/flipkart.md)
* [Walmart](../../company-based-lists/walmart.md)

### Problem Statement

Given a Binary Tree, find the vertical traversal of it starting from the leftmost level to the rightmost level.\
 If there are multiple nodes passing through a vertical line, then they should be printed as they appear in **level order** traversal of the tree.

**Example 1:**

```
Input:
           1
         /   \
       2       3
     /   \   /   \
   4      5 6      7
              \      \
               8      9           
Output: 
4 2 1 5 6 3 8 7 9 
Explanation:


```

![](<../../.gitbook/assets/image (52).png>)

**Example 2:**

```
Input:
       1
    /    \
   2       3
 /    \      \
4      5      6
Output: 4 2 1 5 3 6
```

**Your Task:**\
 You don't need to read input or print anything. Your task is to complete the function **verticalOrder() **which takes the root node as input parameter and returns an array containing the vertical order traversal of the tree from the leftmost to the rightmost level. If 2 nodes lie in the same vertical level, they should be printed in the order they appear in the level order traversal of the tree.

**Expected Time Complexity: **O(N)\
 **Expected Auxiliary Space: **O(N)

**Constraints:**\
 1 <= Number of nodes <= 3\*10^4

### Solution

```cpp
struct nodeWithHorizontalDistance{
    Node *node;
    int hd; // horizontal_distance
    nodeWithHorizontalDistance(Node *root, int my_hd){
        this->node = root;
        this->hd = my_hd;
    }
};
class Solution
{
    public:
    //Function to find the vertical order traversal of Binary Tree. 
    vector<int> verticalOrder(Node *root)
    {
        // DO BFS and update the map elements as per their horizontal distance
        // Queue has treenode and its hd value
        queue<nodeWithHorizontalDistance> q;
        map<int, vector<int>> verticalTraversal;
        nodeWithHorizontalDistance qnode(root, 0);
        q.push(qnode);
        while(q.empty() == false)
        {
            int size = q.size();
            for(int i = size-1; i >= 0; i--)
            {
                nodeWithHorizontalDistance cur = q.front(); q.pop();
                verticalTraversal[cur.hd].push_back(cur.node->data);
                if(cur.node->left != nullptr)
                {
                    nodeWithHorizontalDistance left(cur.node->left, cur.hd-1);
                    q.push(left);
                }
                if(cur.node->right != nullptr)
                {
                    nodeWithHorizontalDistance right(cur.node->right, cur.hd+1);
                    q.push(right);
                }
            }
        }
        vector<int> verticalOrderResult;
        for(auto item = verticalTraversal.begin(); item != verticalTraversal.end(); item++)
        {
            for(int index = 0; index < item->second.size(); index++)
                verticalOrderResult.push_back(item->second[index]);
        }
        
        return verticalOrderResult;
    }
};
```

