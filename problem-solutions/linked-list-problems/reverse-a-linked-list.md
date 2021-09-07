# Reverse a Linked List

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/reverse-a-linked-list/1#)
* [Leetcode 206](https://leetcode.com/problems/reverse-linked-list/)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Samsung](../../company-based-lists/samsung.md)
* [Adobe](../../company-based-lists/adobe.md)

### Problem Statement

Given a linked list of **N** nodes. The task is to reverse this list.

**Example 1:**

```text
Input:
LinkedList: 1->2->3->4->5->6
Output: 6 5 4 3 2 1
Explanation: After reversing the list, 
elements are 6->5->4->3->2->1.
```

**Example 2:**

```text
Input:
LinkedList: 2->7->8->9->10
Output: 10 9 8 7 2
Explanation: After reversing the list,
elements are 10->9->8->7->2.
```

**Expected Time Complexity:** O\(N\).  
**Expected Auxiliary Space:** O\(1\).

**Constraints:**  
 1 &lt;= N &lt;= 10^4

### Solution

```cpp
/* Linked List Node structure:
struct Node
{
    int data;
    struct Node *next;
}
*/

class Solution
{
public:
    struct Node* reverseList(struct Node *head)
    {
        struct Node *temp = head;
        struct Node *prev = NULL, *next = NULL;
        while(temp != NULL){
            next = temp->next;
            temp->next = prev;
            prev = temp;
            temp = next;
        }
        return prev;
    }
};
```

