# Linked Lists

Similar to the array, the linked list is also a **linear** data structure. Here is an example:

![Singly Linked List](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/12/screen-shot-2018-04-12-at-152754.png)

As you can see, each element in the linked list is actually a separate object while all the objects are **linked together by the reference field** in each element.

There are two types of linked list: **singly linked list and doubly linked list**. The example above is a singly linked list and here is an example of doubly linked list:

![Doubly Linked List](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/17/screen-shot-2018-04-17-at-161130.png)

For more details on [Singly Linked List](singly-linked-list/) and [Doubly Linked List](doubly-linked-list/)

### Performance Review

A Singly-linked list is more space efficient than doubly-linked list because nodes do not contain previous field. The trade-off is the inability to do bidirectional iteration.

They are similar in many operations:

1. Both of them are `not able to access the data at a random position` in constant time.
2. Both of them are able to `add a new node after given node or at the beginning of the list in O(1) time`.
3. Both of them are able to `delete the first node in O(1) time`.

But it is a little different to `delete a given node` (including the last node).

* In a singly linked list, it is not able to get the previous node of a given node so we have to spend `O(N)` time to find out the previous node before deleting the given node.
* In a doubly linked list, it will be much easier because we can get the previous node with the "prev" reference field. So we can delete a given node in `O(1)` time.

### Comparing Array, Singly Linked List, Doubly Linked List

Here we provide a comparison of `time complexity` between the linked list and the [array](../arrays/).

![](https://assets.leetcode.com/uploads/2020/10/02/comparison\_of\_time\_complexity.png)

After this comparison, it is not difficult to come up with our conclusion:

> If you need to add or delete a node frequently, a linked list could be a good choice.
>
> If you need to access an element by index often, an array might be a better choice than a linked list.



### C++ Standard Library

For singly linked list, we have [**forward\_list**](https://app.gitbook.com/@thangarajn1992/s/cpp-dictionary/containers/forward-list) **** library. The key functions to remember in this library are

* push\_front
* pop\_front
* emplace\_front
* insert\_after
* emplace\_after
* erase\_after
* splice\_after
* reverse
* sort

For doubly linked list, we have [**list**](https://app.gitbook.com/@thangarajn1992/s/cpp-dictionary/containers/list) **** library. The key functions to remember in this library are

* push\_front
* emplace\_front
* pop\_front
* push\_back
* emplace\_back
* pop\_back
* splice
* reverse
* sort

