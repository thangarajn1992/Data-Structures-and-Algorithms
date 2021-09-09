# Rotate linked list clockwise

### Sources

* [Leetcode 61](https://leetcode.com/problems/rotate-list/)

### Companies

### Problem Statement

Given the `head` of a linked list, rotate the list to the right by `k` places.

**Example 1:** 

![](https://assets.leetcode.com/uploads/2020/11/13/rotate1.jpg)

```text
Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]
```

**Example 2:** 

![](https://assets.leetcode.com/uploads/2020/11/13/roate2.jpg)

```text
Input: head = [0,1,2], k = 4
Output: [2,0,1]
```

**Constraints:**

* The number of nodes in the list is in the range `[0, 500]`.
* `-100 <= Node.val <= 100`
* `0 <= k <= 2 * 10^9`

### Solution

```cpp
class Solution {
public:
    ListNode* rotateRight(ListNode* head, int k) {
        if(!head || !k) 
            return head;
        
        // Find totalNodes and pointer to lastnode 
        // so that we can link it back to head
        int totalNodes = 1;
        ListNode *lastNode  = head;
        while(lastNode->next != nullptr)
        {
            totalNodes++;
            lastNode = lastNode->next;
        }
        k = k % totalNodes;
        if(k == 0)
            return head;
        
        int newHeadDistance = totalNodes - k; // New head distance from head
        
        //pin tail to head 
        lastNode->next = head;
        
        // Find Node prev to newHead
        ListNode *curr = head;
        for(int i = 1; i < newHeadDistance; i++)
            curr = curr->next;
        
        head = curr->next;
        curr->next = nullptr;
        
        return head;        
    }
};
```

