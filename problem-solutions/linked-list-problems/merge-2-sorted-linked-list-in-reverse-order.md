# Merge 2 sorted linked list in reverse order

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/merge-2-sorted-linked-list-in-reverse-order/1)

### Companies

* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given two linked lists of size **N** and **M**, which are sorted in non-decreasing order. The task is to merge them in such a way that the resulting list is in decreasing order. Return the pointer to the merged linked list which is in non-increasing order.

**Constraints:**\
&#x20;1 <=T<= 50\
&#x20;1 <= N, M <= 1000

**Example:**\
&#x20;**Input:**\
&#x20;2\
&#x20;4 3\
&#x20;5 10 15 40 \
&#x20;2 3 20\
&#x20;2 2\
&#x20;1 1\
&#x20;2 4

**Output:**\
&#x20;40 20 15 10 5 3 2\
&#x20;4 2 1 1&#x20;

**Explanation:**\
&#x20;**Testcase 1:** After merging the two lists in decreasing order, we have new lists as 40->20->15->10->5->3->2.

### Solution

```cpp
struct Node * mergeResult(Node *node1,Node *node2)
{
    struct Node *temp1 = node1, *temp2= node2;
    struct Node *result = NULL, *next = NULL;
    
    while(node1 != NULL && node2 != NULL){
        if(node1->data < node2->data) {
            next = node1->next;
            node1->next = result;
            result = node1;
            node1 = next;
        }
        else {
            next = node2->next;
            node2->next = result;
            result = node2;
            node2 = next;
        }
    }
    while(node1)
    {
        next = node1->next;
        node1->next = result;
        result = node1;      
        node1 = next;
    }
    while(node2)
    {
        next = node2->next;
        node2->next = result;
        result = node2;
        node2 = next;
    }
    return result;
}
```
