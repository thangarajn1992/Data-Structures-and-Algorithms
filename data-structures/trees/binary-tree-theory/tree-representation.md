# Tree Representation

### Linked/Dynamic Representation

The dynamic representation is the normal linked representation where each node points to its children using pointers.

### Sequential/Array Representation

In order to represent a tree using an array, the numbering of nodes can start either from 0 – (n-1).

```
       A(0)    
     /   \
    B(1)  C(2)  
  /   \      \
 D(3)  E(4)   F(6) 
```

$$
Parent Index: (ChildIndex-1)/2
$$

$$
Left Child Index: (ParentIndex * 2) + 1
$$

$$
Right Child Index: (ParentIndex * 2) + 2
$$

### Parent Array Representation

An array that represents a tree in such a way that array indexes are values in tree nodes and array values give the parent node of that particular index (or node). The value of the root node index would always be -1 as there is no parent for root.



```
Parent Array Representation  
{1, 5, 5, 2, 2, -1, 3}

Linked Representation
          5
        /  \
       1    2
      /    / \
     0    3   4
         /
        6 
```
