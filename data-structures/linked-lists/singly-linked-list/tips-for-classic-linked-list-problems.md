# Tips for Solving Linked List Problems

* List problems often have a simple brute-force solution that uses O\(N\) space, but a subtler solution that uses the **existing list nodes** to reduce space complexity to O\(1\).
* Very Often, a problem on lists is conceptually simple, and is more about **cleanly coding what's specified**, rather than desiging an algorithm
* Consider using **dummy head** \(sometimes referred as sentinels\) to avoid having to check for empty lists. This simplifies code, and makes bugs less likely.
* It's easy to forget to **update next** for the head and tail.
* Algorithms operating on singly linked lists often benefit from using **two pointers \(iterators\),** one ahead of the other, or advancing quicker than the other.
* **Going through some test cases will save you time :** It is not easy to debug when using a linked list. Therefore, it is always useful to try several different examples on your own to validate your algorithm before writing code.
* **Feel free to use several pointers at the same time.** Sometimes when you design an algorithm for a linked-list problem, there might be several nodes you want to track at the same time. You should keep in mind which nodes you need to track and feel free to use several different pointers to track these nodes at the same time. If you use several pointers, it will be better to give them suitable names in case you have to debug or review your code in the future.
* **In many cases, you need to track the previous node of the current node.** You are not able to trace back the previous node in a singly linked list. So you have to store not only the current node but also the previous node. This is different in a doubly linked list which we will cover in the later chapter.

