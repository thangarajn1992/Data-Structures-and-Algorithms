# Is Palindrome Linked List

### Sources

* [Leetcode 234](https://leetcode.com/problems/palindrome-linked-list/)

### Companies

### Problem Statement

Given the `head` of a singly linked list, return `true` if it is a palindrome.

**Example 1:** ![](https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg)

```text
Input: head = [1,2,2,1]
Output: true
```

**Example 2:** ![](https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg)

```text
Input: head = [1,2]
Output: false
```

**Constraints:**

* The number of nodes in the list is in the range `[1, 10^5]`.
* `0 <= Node.val <= 9`

  **Follow up:** Could you do it in `O(n)` time and `O(1)` space?

### Solution

#### Find Mid Node + Reverse Second Half + Compare two Halves

```cpp
class Solution {
public:
    /* 1. Find the mid element using slow and fast pointers
     * 2. Reverse the second half of linked list starting from mid node
     * 3. Compare first half and second half 
     */
    bool isPalindrome(ListNode* head) {
        if(head == nullptr || head->next == nullptr) 
            return true;
        ListNode* mid = findMid(head);
        ListNode* secondHalfHead = reverseList(mid);
        return compareList(head, secondHalfHead);
    }
    
    ListNode* findMid(ListNode* head){
        ListNode* slow = head, *fast = head;
        while(fast != nullptr && fast->next != nullptr){
            slow = slow->next;
            fast = fast->next->next;;
        }
        return slow;
    }
    ListNode* reverseList(ListNode* head){
        ListNode* prev = nullptr, *curr = head, *temp = nullptr;
        while(curr != NULL){
            temp = curr->next;
            curr->next = prev;
            prev = curr;
            curr = temp;
        } 
        return prev;
    }
    bool compareList(ListNode* head1, ListNode* head2){
        while(head1 != nullptr && head2 != nullptr){
            if(head1->val != head2->val) 
                return false;
            head1 = head1->next;
            head2 = head2->next;
        }
        return true;
    }
};
```

#### Recursive Approach

```cpp
class Solution {
public:    
    bool isPalindromeUtil(ListNode **left, ListNode *right)
    {
        if(right == NULL)
            return 1;
        if(isPalindromeUtil(left, right->next))
        {
            if((*left)->val == right->val){
                (*left) = (*left)->next;
                return 1;
            }
        }
        return 0;
    }
    
    bool isPalindrome(ListNode* head) {
        return isPalindromeUtil(&head, head);
    }
};
```

