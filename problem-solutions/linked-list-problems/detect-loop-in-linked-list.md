# Detect Loop in Linked List

### Sources

* [Leetcode 141](https://leetcode.com/problems/linked-list-cycle/)
* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/detect-loop-in-linked-list/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Samsung](../../company-based-lists/samsung.md)
* [Walmart](../../company-based-lists/walmart.md)
* [Adobe](../../company-based-lists/adobe.md)

### Problem Statement

Given `head`, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to. **Note that `pos` is not passed as a parameter**.

Return `true` _if there is a cycle in the linked list_. Otherwise, return `false`.

**Example 1:** ![](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

```text
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).
```

**Example 2:** ![](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

```text
Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.
```

**Example 3:** ![](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

```text
Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.
```

**Constraints:**

* The number of the nodes in the list is in the range `[0, 10^4]`.
* `-10^5 <= Node.val <= 10^5`
* `pos` is `-1` or a **valid index** in the linked-list.

### Solution

```cpp
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if(!head) 
            return false;
        ListNode *slow = head, *fast = head->next;
        
        while(slow && fast && fast->next && slow != fast){
            slow = slow->next;
            fast = fast->next->next;
        }
        return (slow == fast);
    }
};
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
```

