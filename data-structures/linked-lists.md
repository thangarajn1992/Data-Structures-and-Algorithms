# Linked Lists

Similar to the array, the linked list is also a **linear** data structure. Here is an example:

![Singly Linked List](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/12/screen-shot-2018-04-12-at-152754.png)

As you can see, each element in the linked list is actually a separate object while all the objects are **linked together by the reference field** in each element.

There are two types of linked list: **singly linked list and doubly linked list**. The example above is a singly linked list and here is an example of doubly linked list:

![Doubly Linked List](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/17/screen-shot-2018-04-17-at-161130.png)

## Introduction - Singly Linked List

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

In most cases, we will use the `head` node \(the first node\) to represent the whole list.

## Singly Linked List Operations

### Accessing Elements

Unlike the array, we are not able to access a random element in a singly-linked list in constant time. If we want to get the ith element, we have to traverse from the head node one by one. It takes us `O(N)` time on average to `visit an element by index`, where N is the length of the linked list.

For instance, in the example above, the head is the node 23. The only way to visit the 3rd node is to use the "next" field of the head node to get to the 2nd node \(node 6\); Then with the "next" field of node 6, we are able to visit the 3rd node.

You might wonder why the linked list is useful though it has such a bad performance \(compared to the array\) in accessing data by index. Well it performs better in insert and delete operations which is explained below

### Add Operation

Unlike an array, we don’t need to move all elements past the inserted element. Therefore, you can insert a new node into a linked list in `O(1)` time complexity, which is very efficient.

#### Adding node in the middle

If we want to add a new value after a given node `prev`, we should: 

1. Initialize a new node `cur` with the given value;
2. Link the "next" field of `cur` to prev's next node `next`;
3. Link the "next" field in `prev` to `cur`.

![](../.gitbook/assets/image%20%2846%29.png)

![](../.gitbook/assets/image%20%2848%29.png)

![](../.gitbook/assets/image%20%2844%29.png)

#### Adding Node in the Beginning

As we know, we use the head node `head` to represent the whole list.

So it is essential to update `head` when adding a new node at the beginning of the list.

1. Initialize a new node `cur`;
2. Link the new node to our original head node `head`.
3. Assign `cur` to `head`.

For example, let's add a new node 9 at the beginning of the list.

1. We initialize a new node 9 and link node 9 to current head node 23.
2. Assign node 9 to be our new head.

![](../.gitbook/assets/image%20%2843%29.png)

![](../.gitbook/assets/image%20%2847%29.png)

### Delete Operation

If we want to delete an existing node `cur` from the singly linked list, we can do it in two steps:

1. Find cur's previous node `prev` and its next node `next`;
2. Link `prev` to cur's next node `next`.

![](../.gitbook/assets/image%20%2845%29.png)

![](../.gitbook/assets/image%20%2849%29.png)

In our first step, we need to find out `prev` and `next`. It is easy to find out `next` using the reference field of `cur`. However, we have to traverse the linked list from the head node to find out `prev` which will take `O(N)` time on average, where N is the length of the linked list. So the time complexity of deleting a node will be `O(N)`.

The space complexity is `O(1)` because we only need constant space to store our pointers.

#### Deleting the First Node \(Head\)

If we want to delete the first node, the strategy will be a little different.

As we mentioned before, we use the head node `head` to represent a linked list. Our head is the black node 23 in the example below.

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/19/screen-shot-2018-04-19-at-130024.png)

If we want to delete the first node, we can simply `assign the next node to head`. That is to say, our head will be node 6 after deletion.

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/19/screen-shot-2018-04-19-at-130031.png)

## Design a Linked List

[Leetcode 707](https://leetcode.com/problems/design-linked-list/)

```cpp
class MyLinkedList {
public:
    /** Initialize your data structure here. */
    struct Node{
        int val;
        Node *next;
        Node(int x) : val(x), next(nullptr) {}
    };
    Node *head;
    MyLinkedList() {
        this->head = nullptr;
    }
    
    /** Get the value of the index-th node in the linked list. If the index is invalid, return -1. */
    int get(int index) {
        Node *cur = this->head;
        for(int i = 0; i < index && cur != nullptr; i++)
            cur = cur->next;
        return (cur) ? cur->val : -1;
    }
    
    /** Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list. */
    void addAtHead(int val) {
        Node *cur = new Node(val);
        cur->next = this->head;
        this->head = cur;
    }
    
    /** Append a node of value val to the last element of the linked list. */
    void addAtTail(int val) {
        Node *cur = this->head;
        if(cur == nullptr)
            addAtHead(val);
        else
        {
            while(cur->next != nullptr)
                cur = cur->next;
            cur->next = new Node(val);
        }
    }
    
    /** Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted. */
    void addAtIndex(int index, int val) {
        if(index == 0)
            addAtHead(val);
        else
        {
            Node *prev = this->head;
            for(int i = 0; i < index - 1 && prev; i++)
                prev = prev->next;
            
            if(prev)
            {
                Node *cur = new Node(val);
                cur->next = prev->next;
                prev->next = cur;
            }
        }
    }
    
    /** Delete the index-th node in the linked list, if the index is valid. */
    void deleteAtIndex(int index) {
        if(this->head == nullptr)
            return;
        if(index == 0)
        {
            this->head = this->head->next;
            return;
        }
        Node *cur = this->head;
        for(int i = 0; i < index-1 && cur != nullptr; i++)
            cur = cur->next;
        
        if(cur && cur->next)
            cur->next = cur->next->next;
    }
};

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList* obj = new MyLinkedList();
 * int param_1 = obj->get(index);
 * obj->addAtHead(val);
 * obj->addAtTail(val);
 * obj->addAtIndex(index,val);
 * obj->deleteAtIndex(index);
 */
```

## Two Pointer Technique

> Given a linked list, determine if it has a cycle in it.

You might have come up with the solution using the `hash table`. But there is a more efficient solution using `the two-pointer technique`. Try to think it over by yourself before reading the remaining content.

Imagine there are two runners with different speed. If they are running on a straight path, the fast runner will first arrive at the destination. However, if they are running on a circular track, the fast runner will catch up with the slow runner if they keep running.

That's exactly what we will come across using two pointers with different speed in a linked list:

1. `If there is no cycle, the fast pointer will stop at the end of the linked list.`
2. `If there is a cycle, the fast pointer will eventually meet with the slow pointer.`

So the only remaining problem is:

> What should be the proper speed for the two pointers?

It is a safe choice to move the slow pointer `one step` at a time while moving the fast pointer `two steps` at a time. For each iteration, the fast pointer will move one extra step. **If the length of the cycle is M, after M iterations, the fast pointer will definitely move one more cycle and catch up with the slow pointer**.

### Problems solved using Two Pointer Technique

* [Detect Cycle in Linked List](../problem-solutions/linked-list-problems/detect-loop-in-linked-list.md)
* 
