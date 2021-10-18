# Merge two Binary Search Trees

### Source

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/merge-two-bst-s/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Google](../../company-based-lists/google.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given two BSTs, return elements of both BSTs in **sorted** form.\
 **Example 1:**

```
Input:
BST1:
       5
     /   \
    3     6
   / \
  2   4  
BST2:
        2
      /   \
     1     3
            \
             7
            /
           6
Output: 1 2 2 3 3 4 5 6 6 7
Explanation: 
After merging and sorting the
two BST we get 1 2 2 3 3 4 5 6 6 7.
```

**Example 2:**

```
Input:
BST1:
       12
     /   
    9
   / \    
  6   11
BST2:
      8
    /  \
   5    10
  /
 2
Output: 2 5 6 8 9 10 11 12
Explanation: 
After merging and sorting the
two BST we get 2 5 6 8 9 10 11 12.
```

**Expected Time Complexity: **O(M+N) where M and N are the sizes if the two BSTs.\
**Expected Auxiliary Space: **O(Height of BST1 + Height of BST2).

\
 **Constraints:**\
 1 ≤ Number of Nodes ≤ 10^5

### Solution

```cpp
class Solution
{
    public:
    vector<int> result;
    vector<int> merge(Node *root1, Node *root2)
    {
       stack<Node *> s1;
       stack<Node *> s2;
       Node *c1 = root1;
       Node *c2 = root2;
       
       if(root1 == nullptr)
       {
           inorder(root2);
           return result;
       }
       if(root2 == nullptr)
       {
           inorder(root1);
           return result;
       }
       
       while(c1 || c2 || !s1.empty() || !s2.empty())
       {
           if(c1 || c2)
           {
                if(c1)
                {
                    s1.push(c1);
                    c1 = c1->left;
                }
                if(c2)
                {
                    s2.push(c2);
                    c2 = c2->left;
                }
            }
            else
            {
                if(s1.empty())
                {
                    while(!s2.empty())
                    {
                        c2 = s2.top(); s2.pop();
                        c2->left = nullptr;
                        inorder(c2);
                    }
                    return result;
                }
                if(s2.empty())
                {
                    while(!s1.empty())
                    {
                        c1 = s1.top(); s1.pop();
                        c1->left = nullptr;
                        inorder(c1);
                    }
                    return result;
                }
                c1 = s1.top(); s1.pop();
                c2 = s2.top(); s2.pop();
                
                if(c1->data < c2->data)
                {
                    result.push_back(c1->data);
                    c1 = c1->right;
                    s2.push(c2);
                    c2 = nullptr;
                }
                else
                {
                    result.push_back(c2->data);
                    c2 = c2->right;
                    s1.push(c1);
                    c1 = nullptr;
                }
            }
       }
       return result;
    }
    void inorder(Node *root)
    {
        if(root)
        {
            inorder(root->left);
            result.push_back(root->data);
            inorder(root->right);
        }
    }
};
```
