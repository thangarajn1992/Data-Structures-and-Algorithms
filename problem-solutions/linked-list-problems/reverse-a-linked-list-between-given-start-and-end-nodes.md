# Reverse a Linked List between given start and end nodes

### Sources

* [Leetcode 92](https://leetcode.com/problems/reverse-linked-list-ii/)
* EPI 8.2

### Companies

### Problem Statement

Given the `head` of a singly linked list and two integers `left` and `right` where `left <= right`, reverse the nodes of the list from position `left` to position `right`, and return _the reversed list_.

**Example 1:** 

![](https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg)

```text
Input: head = [1,2,3,4,5], left = 2, right = 4
Output: [1,4,3,2,5]
```

**Example 2:**

```text
Input: head = [5], left = 1, right = 1
Output: [5]
```

**Constraints:**

* The number of nodes in the list is `n`.
* `1 <= n <= 500`
* `-500 <= Node.val <= 500`
* `1 <= left <= right <= n`

### Algorithm

* We identify the start of sublist by using iteration to get the start node and its predecessor.
* Once we reach the start node, we start the reversing process and keep counting.
* When we reach the finish node, we stop the reversion process and link the reverted section with the unreverted section.

### Solution

```cpp
class Solution {
public:
    ListNode* reverseBetween(ListNode* head, int start, int finish) {
        if(start == finish) // no need to reverse
            return head; 
        ListNode *dummyHead = new ListNode(0, head);
        
        // Find the node previous to our sublist start
        ListNode *subListHead = dummyHead;
        int position = 1;
        while(position < start)
        {
            subListHead = subListHead->next;
            position++;
        }

        // Reverse the sublist
        ListNode* subListIter = subListHead->next;
        
        while(start < finish)
        {
            ListNode* temp = subListIter->next;
            subListIter->next = temp->next;
            temp->next = subListHead->next;
            subListHead->next = temp;
            start++;
        }
        return dummyHead->next;
    }
};
```

