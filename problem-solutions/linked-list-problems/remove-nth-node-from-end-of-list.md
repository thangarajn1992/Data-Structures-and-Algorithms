# Remove Nth Node From End of List

### Sources

* [Leetcode 19](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

### Companies

### Problem Statement

Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

**Example 1:** ![](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

```text
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
```

**Example 2:**

```text
Input: head = [1], n = 1
Output: []
```

**Example 3:**

```text
Input: head = [1,2], n = 1
Output: [1]
```

**Constraints:**

* The number of nodes in the list is `sz`.
* `1 <= sz <= 30`
* `0 <= Node.val <= 100`
* `1 <= n <= sz`

**Follow up:** Could you do this in one pass?

### Solution

```cpp
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode dummy = ListNode(0);
        dummy.next = head;
        
        ListNode *fast = &dummy, *slow = &dummy;
        for(int i = 0; i <= n; i++) {
            fast = fast->next;
        }
        while(fast != nullptr) {
            fast = fast->next;
            slow = slow->next;
        }
        slow->next = slow->next->next;
        return dummy.next;
    }
};
```

