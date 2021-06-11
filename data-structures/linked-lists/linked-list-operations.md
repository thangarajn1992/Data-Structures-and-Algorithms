# Linked List Operations



### Reverse a Linked List

[GeeksForGeeks Link](https://practice.geeksforgeeks.org/problems/reverse-a-linked-list/1#)

[Leetcode Link](https://leetcode.com/problems/reverse-linked-list/)

```cpp
struct Node* reverseList(struct Node *head)
{
    struct Node *curr = head;
    struct Node *prev = NULL, *next = NULL;
    while(curr != NULL){
        next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}
```



