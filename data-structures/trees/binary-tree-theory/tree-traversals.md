---
description: Different Types of Traversals in Tree
---

# Tree Traversals

### Pre-Order Traversal

Pre-order traversal is to visit the root first. Then traverse the left sub-tree. Finally, traverse the right sub-tree. Here is an example:

![Pre order Traversal](<../../../.gitbook/assets/image (62).png>)

#### Benefits of Pre order Traversal

* Pre order traversal is used to create a copy of the tree.&#x20;
* Pre order traversal is also used to get prefix expression on an expression tree

### In-Order Traversal

In-order traversal is to traverse the left sub-tree first. Then visit the root. Finally, traverse the right sub-tree. Typically, for `binary search tree`, we can retrieve all the data in sorted order using in-order traversal.

![In order Traversal](<../../../.gitbook/assets/image (57).png>)

#### Benefits of In order Traversal:

* In Binary Search Tree, in order traversal gives nodes in non-decreasing order.

### Post Order Traversal

Post-order traversal is to traverse the left sub-tree first. Then traverse the right sub-tree. Finally, visit the root.

![Post Order Traversal](<../../../.gitbook/assets/image (58).png>)

#### Benefits of Post Order Traversal

It is worth noting that when you delete nodes in a tree, deletion process will be in post-order. That is to say, when you delete a node, you will delete its left child and its right child before you delete the node itself.

Also, post-order is widely use in mathematical expression. It is easier to write a program to parse a post-fix expression of an expression tree. Here is an example:

![Post Order Mathematical Expression](<../../../.gitbook/assets/image (65).png>)

You can easily figure out the original expression using the in-order traversal. However, it is not easy for a program to handle this expression since you have to check the priorities of operations.

If you handle this tree in post-order, you can easily handle the expression using a stack. Each time when you meet a operator, you can just pop 2 elements from the stack, calculate the result and push the result back into the stack.



### Level Order Traversal

Level-order traversal is to traverse the tree level by level.

`Breadth-First Search` is an algorithm to traverse or search in data structures like a tree or a graph. The algorithm starts with a root node and visit the node itself first. Then traverse its neighbors, traverse its second level neighbors, traverse its third level neighbors, so on and so forth.

When we do breadth-first search in a tree, the order of the nodes we visited is in level order. Typically, we use a queue to help us to do BFS.

![Level Order Traversal](<../../../.gitbook/assets/image (60).png>)

### Zig-Zag Traversal



### Spiral Traversal



### Boundary Traversal



### Diagonal Traversal

### Morris Traversal - Inorder without recursion and stack

Using Morris Traversal, we can traverse the tree without using stack and recursion. The idea of Morris Traversal is based on Threaded Binary Tree. In this traversal, we first create links to Inorder successor and print the data using these links, and finally revert the changes to restore original tree.&#x20;

```cpp
    vector<int> inorderIterativeMorris(BinaryTreeNode *root)
    {
        BinaryTreeNode* curr = root;
        vector<int> inorder;
        while(curr != nullptr)
        {
            /* If no left, print curr and move to its right */
            if(curr->left == nullptr)
            {
                inorder.push_back(curr->data);
                curr = curr->right;
            }
            else
            {
                BinaryTreeNode *pre = curr->left;
                /* Move the rightmost node which will be predecessor 
                   of current in inorder traversal */
                while(pre->right != nullptr && pre->right != curr)
                {
                    pre = pre->right;
                }

                /* If we are visiting for first time, make current as prev
                   right pointer */
                if(pre->right == nullptr)
                {
                    pre->right = curr;
                    curr = curr->left;
                }
                else /* We are reaching here for second time, reset the right ptr */ 
                {
                    pre->right = nullptr;
                    inorder.push_back(curr->data);
                    curr = curr->right;
                }
            }
        }
        return inorder;
    }
```
