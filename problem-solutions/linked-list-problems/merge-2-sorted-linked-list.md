# Merge 2 Sorted Linked List

### Sources

* [Leetcode 21](https://leetcode.com/problems/merge-two-sorted-lists/)

### Companies

### Problem Statement

Merge two sorted linked lists and return it as a **sorted** list. The list should be made by splicing together the nodes of the first two lists.

**Example 1:** 

![](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

```text
Input: l1 = [1,2,4], l2 = [1,3,4]
Output: [1,1,2,3,4,4]
```

**Example 2:**

```text
Input: l1 = [], l2 = []
Output: []
```

**Example 3:**

```text
Input: l1 = [], l2 = [0]
Output: [0]
```

**Constraints:**

* The number of nodes in both lists is in the range `[0, 50]`.
* `-100 <= Node.val <= 100`
* Both `l1` and `l2` are sorted in **non-decreasing** order.

### Solution

```cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* result = new ListNode();
        ListNode* l3 = result;
        while(l1 && l2)
        {
            if(l1->val <= l2->val)
            {
                l3->next = l1;
                l1 = l1->next;
            }
            else
            {
                l3->next = l2;
                l2 = l2->next;
            }
            l3 = l3->next;
        }
        l3->next = (l1 != nullptr) ? l1 : l2;
        return result->next;
    }
};
```

