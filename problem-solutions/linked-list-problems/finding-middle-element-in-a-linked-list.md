# Finding middle element in a linked list

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/finding-middle-element-in-a-linked-list/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Flipkart](../../company-based-lists/flipkart.md)
* [Samsung](../../company-based-lists/samsung.md)
* [Adobe](../../company-based-lists/adobe.md)

### Problem Statement

Given a singly linked list of **N** nodes.The task is to find the **middle** of the linked list. For example, if the linked list is **1-&gt; 2-&gt;3-&gt;4-&gt;5**, ****then the middle node of the list is **3**. If there are two middle nodes\(in case, when **N** is even\), print the **second middle** element. For example, if the linked list given is **1-&gt;2-&gt;3-&gt;4-&gt;5-&gt;6**, then the middle node of the list is **4**.

**Example 1:**

```text
Input:
LinkedList: 1->2->3->4->5
Output: 3 
Explanation: 
Middle of linked list is 3.
```

**Example 2:** 

```text
Input:
LinkedList: 2->4->6->7->5->1
Output: 7 
Explanation: 
Middle of linked list is 7.
```

**Expected Time Complexity:** O\(N\).  
**Expected Auxiliary Space:** O\(1\).

**Constraints:**  
 1 &lt;= N &lt;= 5000

### Solution

```cpp
class Solution{
public:
    /* Should return data of middle node. If linked list is empty, then  -1*/
    int getMiddle(Node *head)
    {
        if(head == nullptr)
            return -1;
        Node* slow = head, *fast = head;
        while(fast != nullptr && fast->next != nullptr)
        {
            slow = slow->next;
            fast = fast->next->next;
        }
        return slow->data;
    }
};
```
