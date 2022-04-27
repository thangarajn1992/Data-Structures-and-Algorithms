---
description: Different Types of Traversals in Tree
---

# Tree Traversals

### Pre-Order Traversal

Pre-order traversal is to visit the root first. Then traverse the left sub-tree. Finally, traverse the right sub-tree. Here is an example:

![Pre order Traversal](<../../../.gitbook/assets/image (59).png>)

### In-Order Traversal

In-order traversal is to traverse the left sub-tree first. Then visit the root. Finally, traverse the right sub-tree. Typically, for `binary search tree`, we can retrieve all the data in sorted order using in-order traversal.

![In order Traversal](<../../../.gitbook/assets/image (56).png>)

### Post Order Traversal

Post-order traversal is to traverse the left sub-tree first. Then traverse the right sub-tree. Finally, visit the root.

![Post Order Traversal](<../../../.gitbook/assets/image (57).png>)

It is worth noting that when you delete nodes in a tree, deletion process will be in post-order. That is to say, when you delete a node, you will delete its left child and its right child before you delete the node itself.

Also, post-order is widely use in mathematical expression. It is easier to write a program to parse a post-order expression. Here is an example:

![Post Order Mathematical Expression](<../../../.gitbook/assets/image (61).png>)

You can easily figure out the original expression using the in-order traversal. However, it is not easy for a program to handle this expression since you have to check the priorities of operations.

If you handle this tree in post-order, you can easily handle the expression using a stack. Each time when you meet a operator, you can just pop 2 elements from the stack, calculate the result and push the result back into the stack.

### Level Order Traversal

Level-order traversal is to traverse the tree level by level.

`Breadth-First Search` is an algorithm to traverse or search in data structures like a tree or a graph. The algorithm starts with a root node and visit the node itself first. Then traverse its neighbors, traverse its second level neighbors, traverse its third level neighbors, so on and so forth.

When we do breadth-first search in a tree, the order of the nodes we visited is in level order. Typically, we use a queue to help us to do BFS.

![Level Order Traversal](<../../../.gitbook/assets/image (58).png>)

### Zig-Zag Traversal



### Spiral Traversal



### Boundary Traversal



### Diagonal Traversal

