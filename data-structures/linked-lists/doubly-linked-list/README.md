# Doubly Linked List

The doubly linked list works in a similar way as Singly linked list but has `one more reference field` which is known as `the "prev" field`. With this extra field, you are able to know the previous node of the current node.

Let's take a look at an example:

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/17/screen-shot-2018-04-17-at-161130.png)

The green arrows indicate how our "prev" field works.

### Node Structure

```cpp
// Definition for doubly-linked list.
struct DoublyListNode {
    int val;
    DoublyListNode *next, *prev;
    DoublyListNode(int x) : val(x), next(NULL), prev(NULL) {}
};
```

Similar to the singly linked list, we will use the `head` node to represent the whole list.

### Operations

We can access data in the same exact way as in a singly linked list:

1. We are `not able to access a random position` in constant time.
2. We have to `traverse from the head` to get the `i-th` node we want.
3. The time complexity in the worse case will be `O(N)`, where `N` is the length of the linked list.

For addition and deletion, it will be a little more complicated since we need to take care of the "prev" field as well.

#### Add Operation

If we want to insert a new node `cur` after an existing node `prev`, we can divide this process into two steps:

1. link `cur` with `prev` and `next`, where `next` is the original next node of `prev`;
2. re-link the `prev` and `next` with `cur`. 

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/28/screen-shot-2018-04-28-at-173045.png)

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/29/screen-shot-2018-04-28-at-173055.png)

Similar to the singly linked list, both the time and the space complexity of the add operation are `O(1)`.

#### Delete Operation

If we want to delete an existing node `cur` from the doubly linked list, we can simply link its previous node `prev` with its next node `next`.

> Unlike the singly linked list, it is easy to get the previous node in constant time with the "prev" field.

Since we no longer need to traverse the linked list to get the previous node, both the time and space complexity are `O(1)`.

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/17/screen-shot-2018-04-17-at-161130.png)

Our goal is to delete the node 6 from the doubly linked list.

So we link its previous node 23 and its next node 15:

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/18/screen-shot-2018-04-18-at-142428.png)

Node 6 is not in our doubly linked list now.



