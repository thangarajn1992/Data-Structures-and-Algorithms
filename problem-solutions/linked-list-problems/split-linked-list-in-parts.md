# Split Linked List in Parts

### Sources

* [Leetcode 725](https://leetcode.com/problems/split-linked-list-in-parts/)

### Companies

### Problem Statement

Given the `head` of a singly linked list and an integer `k`, split the linked list into `k` consecutive linked list parts.

The length of each part should be as equal as possible: no two parts should have a size differing by more than one. This may lead to some parts being null.

The parts should be in the order of occurrence in the input list, and parts occurring earlier should always have a size greater than or equal to parts occurring later.

Return _an array of the_ `k` _parts_.

**Example 1:** ![](https://assets.leetcode.com/uploads/2021/06/13/split1-lc.jpg)

```text
Input: head = [1,2,3], k = 5
Output: [[1],[2],[3],[],[]]
Explanation:
The first element output[0] has output[0].val = 1, output[0].next = null.
The last element output[4] is null, but its string representation as a ListNode is [].
```

**Example 2:** 

![](https://assets.leetcode.com/uploads/2021/06/13/split2-lc.jpg)

```text
Input: head = [1,2,3,4,5,6,7,8,9,10], k = 3
Output: [[1,2,3,4],[5,6,7],[8,9,10]]
Explanation:
The input has been split into consecutive parts with size difference at most 1, and earlier parts are a larger size than the later parts.
```

**Constraints:**

* The number of nodes in the list is in the range `[0, 1000]`.
* `0 <= Node.val <= 1000`
* `1 <= k <= 50`



### Solution

```cpp
class Solution {
public:
    vector<ListNode*> splitListToParts(ListNode* head, int k) {
        int totalNodes = 0;
        ListNode* curr = nullptr;
        
        // Find total number of nodes
        for(curr = head; curr != nullptr; curr = curr->next)
            totalNodes++;
        
        // Each part will have total/k nodes and
        // total%k parts will have one extra nodes.
        int nodesInEachPart = totalNodes/k;
        int partsWithExtraNodes = totalNodes%k;
        
        // Initialize all the parts with nullptr.
        vector<ListNode *> result(k, nullptr);
        int partNum = 0;
        curr = head;
        
        while(curr != nullptr && partNum < k)
        {
            int nodesInThisPart = nodesInEachPart + ((partNum < partsWithExtraNodes) ? 1 : 0);
            result[partNum] = curr;
            int nodeNum = 1;
            while(curr && nodeNum < nodesInThisPart)
            {
                curr = curr->next;
                nodeNum++;
            }
            // Mark this part's last node's next as null 
            if(curr)
            {
                ListNode *temp = curr->next;
                curr->next = nullptr;
                curr = temp;
            }
            partNum++;
        } 
        return result;
    }
};
```

