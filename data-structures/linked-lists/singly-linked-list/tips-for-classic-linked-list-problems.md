# Tips for Classic Linked List Problems

**1. Going through some test cases will save you time.**

It is not easy to debug when using a linked list. Therefore, it is always useful to try several different examples on your own to validate your algorithm before writing code.

**2. Feel free to use several pointers at the same time.**

Sometimes when you design an algorithm for a linked-list problem, there might be several nodes you want to track at the same time. You should keep in mind which nodes you need to track and feel free to use several different pointers to track these nodes at the same time.

If you use several pointers, it will be better to give them suitable names in case you have to debug or review your code in the future.

**3. In many cases, you need to track the previous node of the current node.**

You are not able to trace back the previous node in a singly linked list. So you have to store not only the current node but also the previous node. This is different in a doubly linked list which we will cover in the later chapter.

