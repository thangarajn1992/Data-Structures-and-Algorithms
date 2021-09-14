# Remove loop in Linked List

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/remove-loop-in-linked-list/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Adobe](../../company-based-lists/adobe.md)
* [Walmart](../../company-based-lists/walmart.md)

### Problem Statement

Given a linked list of **N** nodes such that it may contain a loop.

> A loop here means that the last node of the link list is connected to the node at position X. If the link list does not have any loop, X=0.

Remove the loop from the linked list, if it is present. Complete the function **removeLoop**\(\) which takes the head of the linked list as input parameter. Simply remove the loop in the list \(if present\) without disconnecting any nodes from the list. **Note:** The generated output will be **1** if your submitted code is correct.

  
 **Example 1:**

```text
Input:
N = 3
value[] = {1,3,4}
X = 2
Output: 1
Explanation: The link list looks like
1 -> 3 -> 4
     ^    |
     |____|    
A loop is present. If you remove it 
successfully, the answer will be 1. 
```

  
 **Example 2:**

```text
Input:
N = 4
value[] = {1,8,3,4}
X = 0
Output: 1
Explanation: The Linked list does not 
contains any loop. 
```

**Expected time complexity :** O\(N\)  
**Expected auxiliary space :** O\(1\)  
**Constraints:**  
 1 ≤ N ≤ 10^4

### Solution

```cpp
class Solution
{
    public:
    void removeLoop(Node* head)
    {
        Node* slow = head, *fast = head, *prev = nullptr;
        while(fast && fast->next)
        {
            slow = slow->next;
            prev = fast->next;
            fast = fast->next->next;
            if(slow == fast)
                break;
        }
        if(slow != fast) // no loop
            return;
        
        slow = head;
        while(slow != fast)
        {
            slow = slow->next;
            prev = fast;
            fast = fast->next;
        }
        
        // slow and fast will point to the node to which loop is connected to.
        // Prev will point to the actual last node of the list 
        // when the loop is removed.
        prev->next = nullptr;
        return;
            
    }
};
```



