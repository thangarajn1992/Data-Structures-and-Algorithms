# Singly Linked List

Each node in a singly-linked list contains not only the value but also **a reference field** to link to the next node. By this way, the singly-linked list organizes all the nodes in a sequence.

Here is an example of a singly-linked list:

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/12/screen-shot-2018-04-12-at-152754.png)

The blue arrows show how nodes in a singly linked list are combined together.

### Node Structure

```cpp
// Definition for singly-linked list.
struct SinglyListNode {
    int val;
    SinglyListNode *next;
    SinglyListNode(int x) : val(x), next(NULL) {}
};
```

In most cases, we will use the `head` node (the first node) to represent the whole list.

## Singly Linked List Operations

### Accessing Elements

Unlike the array, we are not able to access a random element in a singly-linked list in constant time. If we want to get the ith element, we have to traverse from the head node one by one. It takes us `O(N)` time on average to `visit an element by index`, where N is the length of the linked list.

For instance, in the example above, the head is the node 23. The only way to visit the 3rd node is to use the "next" field of the head node to get to the 2nd node (node 6); Then with the "next" field of node 6, we are able to visit the 3rd node.

You might wonder why the linked list is useful though it has such a bad performance (compared to the array) in accessing data by index. Well it performs better in insert and delete operations which is explained below

### Add Operation

Unlike an array, we don’t need to move all elements past the inserted element. Therefore, you can insert a new node into a linked list in `O(1)` time complexity, which is very efficient.

#### Adding node in the middle

If we want to add a new value after a given node `prev`, we should:&#x20;

1. Initialize a new node `cur` with the given value;
2. Link the "next" field of `cur` to prev's next node `next`;
3. Link the "next" field in `prev` to `cur`.

![](<../../../.gitbook/assets/image (43).png>)

![](<../../../.gitbook/assets/image (44).png>)

![](<../../../.gitbook/assets/image (45).png>)

#### Adding Node in the Beginning

As we know, we use the head node `head` to represent the whole list.

So it is essential to update `head` when adding a new node at the beginning of the list.

1. Initialize a new node `cur`;
2. Link the new node to our original head node `head`.
3. Assign `cur` to `head`.

For example, let's add a new node 9 at the beginning of the list.

1. We initialize a new node 9 and link node 9 to current head node 23.
2. Assign node 9 to be our new head.

![](<../../../.gitbook/assets/image (46).png>)

![](<../../../.gitbook/assets/image (47).png>)

### Delete Operation

If we want to delete an existing node `cur` from the singly linked list, we can do it in two steps:

1. Find cur's previous node `prev` and its next node `next`;
2. Link `prev` to cur's next node `next`.

![](<../../../.gitbook/assets/image (48).png>)

![](<../../../.gitbook/assets/image (49).png>)

In our first step, we need to find out `prev` and `next`. It is easy to find out `next` using the reference field of `cur`. However, we have to traverse the linked list from the head node to find out `prev` which will take `O(N)` time on average, where N is the length of the linked list. So the time complexity of deleting a node will be `O(N)`.

The space complexity is `O(1)` because we only need constant space to store our pointers.

#### Deleting the First Node (Head)

If we want to delete the first node, the strategy will be a little different.

As we mentioned before, we use the head node `head` to represent a linked list. Our head is the black node 23 in the example below.

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/19/screen-shot-2018-04-19-at-130024.png)

If we want to delete the first node, we can simply `assign the next node to head`. That is to say, our head will be node 6 after deletion.

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/19/screen-shot-2018-04-19-at-130031.png)



