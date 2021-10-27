# Binary Tree Theory

A `tree` is a frequently-used data structure to simulate a hierarchical tree structure.

Each node of the tree will have a root value and a list of references to other nodes which are called child nodes. From graph view, a tree can also be defined as a directed acyclic graph which has `N nodes` and `N-1 edges`.

&#x20;A `Binary Tree` is one of the most typical tree structure. As the name suggests, a binary tree is a tree data structure in which each node has `at most two children`, which are referred to as the left child and the right child.

## Tree Traversal

### Pre Order Traversal

Pre-order traversal is to visit the root first. Then traverse the left subtree. Finally, traverse the right subtree. Here is an example:

![](<../../.gitbook/assets/Screenshot 2021-10-04 at 5.29.43 PM.png>)

### In Order Traversal

In-order traversal is to traverse the left subtree first. Then visit the root. Finally, traverse the right subtree. Typically, for `binary search tree`, we can retrieve all the data in sorted order using in-order traversal.

![](<../../.gitbook/assets/Screenshot 2021-10-04 at 5.30.22 PM.png>)

### Post Order Traversal

Post-order traversal is to traverse the left subtree first. Then traverse the right subtree. Finally, visit the root.

![](<../../.gitbook/assets/Screenshot 2021-10-04 at 5.31.35 PM.png>)

It is worth noting that when you delete nodes in a tree, deletion process will be in post-order. That is to say, when you delete a node, you will delete its left child and its right child before you delete the node itself.

Also, post-order is widely use in mathematical expression. It is easier to write a program to parse a post-order expression. Here is an example:

![](https://leetcode.com/explore/learn/card/data-structure-tree/134/traverse-a-tree/Figures/binary\_tree/mathematical\_expression.png)

You can easily figure out the original expression using the inorder traversal. However, it is not easy for a program to handle this expression since you have to check the priorities of operations.

If you handle this tree in postorder, you can easily handle the expression using a stack. Each time when you meet a operator, you can just pop 2 elements from the stack, calculate the result and push the result back into the stack.

### Level Order Traversal

Level-order traversal is to traverse the tree level by level.

`Breadth-First Search` is an algorithm to traverse or search in data structures like a tree or a graph. The algorithm starts with a root node and visit the node itself first. Then traverse its neighbors, traverse its second level neighbors, traverse its third level neighbors, so on and so forth.

When we do breadth-first search in a tree, the order of the nodes we visited is in level order. Typically, we use a queue to help us to do BFS.

![](<../../.gitbook/assets/Screenshot 2021-10-04 at 6.27.49 PM.png>)

