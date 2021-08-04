# Linked Lists



## Linked List Operations

* Insert Element in Linked List
* Remove Element in Linked List
* [Reverse a Linked List](linked-lists.md#reverse-a-linked-list)

### Reverse a Linked List

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

