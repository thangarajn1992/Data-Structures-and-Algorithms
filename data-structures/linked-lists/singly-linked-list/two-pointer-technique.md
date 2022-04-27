# Two Pointer Technique

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

* [Detect Loop in Linked List](../../../problem-solutions/linked-list-problems/detect-loop-in-linked-list.md)
* [Detect the Node where Loop begins in linked list](../../../problem-solutions/linked-list-problems/detect-the-node-where-loop-begins-in-linked-list.md)
* [Intersection Point in Y Shaped Linked Lists](../../../problem-solutions/linked-list-problems/intersection-point-in-y-shaped-linked-lists.md)
* [Remove Nth Node From End of List](../../../problem-solutions/linked-list-problems/remove-nth-node-from-end-of-list.md)

### Summary for Two Pointer Technique

It is similar to what we have learned in an array. But it can be trickier and error-prone. There are several things you should pay attention:

**1. Always examine if the node is null before you call the next field.**

Getting the next node of a null node will cause the null-pointer error. For example, before we run `fast = fast.next.next`, we need to examine both `fast` and `fast.next` is not null.

**2. Carefully define the end conditions of your loop.**

Run several examples to make sure your end conditions will not result in an endless loop. And you have to take our first tip into consideration when you define your end conditions.

#### Complexity Analysis

It is easy to analyze the space complexity. If you only use pointers without any other extra space, the space complexity will be `O(1)`. However, it is more difficult to analyze the time complexity. In order to get the answer, we need to analyze `how many times we will run our loop` .

In our previous finding cycle example, let's assume that we move the faster pointer 2 steps each time and move the slower pointer 1 step each time.

1. If there is no cycle, the fast pointer takes `N/2 times` to reach the end of the linked list, where N is the length of the linked list.
2. If there is a cycle, the fast pointer needs `M times` to catch up the slower pointer, where M is the length of the cycle in the list.

Obviously, M <= N. So we will run the loop `up to N times`. And for each loop, we only need constant time. So, the time complexity of this algorithm is `O(N)` in total.

Analyze other problems by yourself to improve your analysis skill. Don't forget to take different conditions into consideration. If it is hard to analyze for all situations, consider the worst one.
