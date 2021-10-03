# Remove all elements with given value in the linked list

### Sources

* [Leetcode 203](https://leetcode.com/problems/remove-linked-list-elements/)

### Companies

### Problem Statement

Given the `head` of a linked list and an integer `val`, remove all the nodes of the linked list that has `Node.val == val`, and return _the new head_.

**Example 1:** 

![](https://assets.leetcode.com/uploads/2021/03/06/removelinked-list.jpg)

```text
Input: head = [1,2,6,3,4,5,6], val = 6
Output: [1,2,3,4,5]
```

**Example 2:**

```text
Input: head = [], val = 1
Output: []
```

**Example 3:**

```text
Input: head = [7,7,7,7], val = 7
Output: []
```

**Constraints:**

* The number of nodes in the list is in the range `[0, 10^4]`.
* `1 <= Node.val <= 50`
* `0 <= val <= 50`

### Solution

```cpp
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        if(head == nullptr || val == 0)
            return head;
        
        ListNode *dummy = new ListNode(0);
        dummy->next = head;
        
        ListNode *curr = dummy;
        while(curr->next)
        {
            if(curr->next->val == val) // remove this node
                curr->next = curr->next->next;
            else
                curr = curr->next;
        }
        return dummy->next;
    }
};
```

