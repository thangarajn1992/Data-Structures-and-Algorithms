# Add Two Numbers represented as linked list with node for each digit

### Sources

* [Leetcode 2](https://leetcode.com/problems/add-two-numbers/)

### Companies

### Problem Statement

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:** 

![](https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg)

```text
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```

**Example 2:**

```text
Input: l1 = [0], l2 = [0]
Output: [0]
```

**Example 3:**

```text
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

**Constraints:**

* The number of nodes in each linked list is in the range `[1, 100]`.
* `0 <= Node.val <= 9`
* It is guaranteed that the list represents a number that does not have leading zeros.

### Solution

```cpp
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode *dummy = new ListNode(0);
        ListNode *curr = dummy;
        int carry = 0;
        while(l1 || l2)
        {
            int x = (l1)? l1->val : 0;
            int y = (l2)? l2->val : 0;
            int sum = x + y + carry;
            carry = sum/10;
            curr->next = new ListNode(sum % 10);
            curr = curr->next;
            if(l1) l1 = l1->next;
            if(l2) l2 = l2->next;
        }
        if(carry)
            curr->next = new ListNode(carry);
        return dummy->next;
    }
};
```

