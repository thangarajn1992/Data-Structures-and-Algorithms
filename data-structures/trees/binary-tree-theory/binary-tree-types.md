---
description: Different Types of Binary Trees
---

# Binary Tree Types

### Full Binary Tree

A Binary Tree is a full binary tree if every node has 0 or 2 children. We can also say a full binary tree is a binary tree in which all nodes except leaf nodes have two children.

![Full Binary Tree](<../../../.gitbook/assets/image (69).png>)

### Complete Binary Tree

A Binary Tree is a Complete Binary Tree if all the levels are completely filled except possibly the last level and the last level has all keys as left as possible.

![Complete Binary Tree](<../../../.gitbook/assets/image (66).png>)

### Perfect Binary Tree

A Binary tree is a Perfect Binary Tree in which all the internal nodes have two children and all leaf nodes are at the same level.

![Perfect Binary Tree](<../../../.gitbook/assets/image (67).png>)

### Balanced Binary Tree

A binary tree is balanced if the height of the tree is O(Log n) where n is the number of nodes. For Example, the AVL tree maintains O(Log n) height by making sure that the difference between the heights of the left and right sub-trees is at most 1. Red-Black trees maintain O(Log n) height by making sure that the number of Black nodes on every root to leaf paths is the same and there are no adjacent red nodes. Balanced Binary Search trees are performance-wise good as they provide O(log n) time for search, insert and delete.

![Balanced Binary Tree](<../../../.gitbook/assets/image (68).png>)

### Degenerate Binary Tree

A Tree where every internal node has one child. Such trees are performance-wise same as linked list.

![Degenerate Binary Tree](<../../../.gitbook/assets/image (63).png>)



### Unlabelled Binary Tree

If nodes in the binary tree are not labelled, then it is unlabelled Binary Tree

```
    o                 o
  /   \             /   \ 
 o     o           o     o 
```

### Labelled Binary Tree

A Binary Tree is labeled if every node is assigned a label.

```
    A                C
  /   \             /  \ 
 B     C           A    B 
```
