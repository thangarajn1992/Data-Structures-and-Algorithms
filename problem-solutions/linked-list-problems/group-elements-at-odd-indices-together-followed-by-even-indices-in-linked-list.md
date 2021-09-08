# Group Elements at Odd Indices together followed by Even indices in linked list

### Sources

* [Leetcode 328](https://leetcode.com/problems/odd-even-linked-list/)

### Companies

### Problem Statement

Given the `head` of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return _the reordered list_.

The **first** node is considered **odd**, and the **second** node is **even**, and so on.

Note that the relative order inside both the even and odd groups should remain as it was in the input.

You must solve the problem in `O(1)` extra space complexity and `O(n)` time complexity.

**Example 1:** ![](https://assets.leetcode.com/uploads/2021/03/10/oddeven-linked-list.jpg)

```text
Input: head = [1,2,3,4,5]
Output: [1,3,5,2,4]
```

**Example 2:** ![](https://assets.leetcode.com/uploads/2021/03/10/oddeven2-linked-list.jpg)

```text
Input: head = [2,1,3,5,6,4,7]
Output: [2,3,6,7,1,5,4]
```

**Constraints:**

* `n ==` number of nodes in the linked list
* `0 <= n <= 10^4`
* `-10^6 <= Node.val <= 10^6`

### Solution

```cpp
class Solution {
public:
    ListNode* oddEvenList(ListNode* head) {
        if(head == nullptr)
            return head;
        ListNode *curOdd = head, *curEven = head->next, *evenHead = head->next;
        while(curEven && curEven->next)
        {
            curOdd->next = curEven->next;
            curOdd = curOdd->next;
            curEven->next = curOdd->next;
            curEven = curEven->next;
        }
        curOdd->next = evenHead;
        return head;
    }
};
```

