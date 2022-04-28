---
description: Properties of Binary Tree
---

# Tree Properties

1. The Number of nodes at level L in binary Tree is $$2^{L}$$. Level of root is 0.
2. The Maximum number of nodes in binary tree  of Height H is $$2^H - 1$$. Height of root only tree is 1.
3. _In a Binary Tree with N nodes, minimum possible height or_ the _minimum number of levels is_ $$Log_{2}\left ( N+1 \right )$$.&#x20;
4. A Binary Tree with L leaves, will have atleast  $$Log_{2}\left ( L \right ) + 1$$levels/height
5. Based on Handshaking lemma, in a binary tree with nodes having either 0 or 2 children, the number of leaves is always 1 higher than the number of nodes with 2 children. $$L = I + 1$$
6. If we extend the above principle to k-ary tree with nodes having either 0 or K children, then number of leaves is $$L =\left (   \left ( K - 1 \right ) * I \right ) + 1$$
7.

### Enumeration

With N nodes, the number of different [unlabelled binary trees](binary-tree-types.md#unlablled-binary-tree) that can be formed is an [nth Catalan Number](../../mathematics/nth-catalan-number.md) which can be calculated using

$$
C_{n} = \frac{2n!}{n! \left ( n+1 \right )!}
$$

Each unlabelled binary tree can produce N! [labelled binary tree](binary-tree-types.md#labelled-binary-tree). Hence with N nodes, the number of different labelled binary trees that can be formed is

$$
C_{n} = \frac{2n!}{n! \left ( n+1 \right )!}\times n!
$$

&#x20;&#x20;
