# Design Doubly Linked List

[Leetcode 707](https://leetcode.com/problems/design-linked-list/)

```cpp
/* Doubly Linked List */
class MyLinkedList {
public:
    /** Initialize your data structure here. */
    struct Node{
        int val;
        Node *prev;
        Node *next;
        Node(int x) : val(x), prev(nullptr), next(nullptr){}
    };
    Node *head;
    MyLinkedList() {
        this->head = nullptr;
    }
    
    /** Get the value of the index-th node in the linked list. If the index is invalid, return -1. */
    int get(int index) {
        Node *cur = this->head;
        for(int i = 0; i < index && cur != nullptr; i++)
            cur = cur->next;
        return (cur) ? cur->val : -1;
    }
    
    /** Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list. */
    void addAtHead(int val) {
        Node *cur = new Node(val);
        if(this->head)
            this->head->prev = cur;
        
        cur->next = this->head;
        this->head = cur;
    }
    
    /** Append a node of value val to the last element of the linked list. */
    void addAtTail(int val) {
        Node *cur = this->head;
        if(cur == nullptr)
            addAtHead(val);
        else
        {
            while(cur->next != nullptr)
                cur = cur->next;
            Node *newNode = new Node(val);
            newNode->prev = cur;
            cur->next = newNode;
        }
    }
    
    /** Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted. */
    void addAtIndex(int index, int val) {
        if(index == 0)
            addAtHead(val);
        else
        {
            Node *prev = this->head;
            for(int i = 0; i < index - 1 && prev; i++)
                prev = prev->next;
            
            if(prev)
            {
                Node *NewNode = new Node(val);
                NewNode->next = prev->next;
                if(prev->next)
                    prev->next->prev = NewNode;
                prev->next = NewNode;
                NewNode->prev = prev;
            }
        }
    }
    
    /** Delete the index-th node in the linked list, if the index is valid. */
    void deleteAtIndex(int index) {
        if(this->head == nullptr)
            return;
        if(index == 0)
        {
            Node *newHead = this->head->next;
            if(newHead)
                newHead->prev = nullptr;
            this->head = newHead;
            return;
        }
        Node *cur = this->head;
        for(int i = 0; i < index-1 && cur != nullptr; i++)
            cur = cur->next;
        
        if(cur && cur->next)
        {
            Node *toDelete = cur->next;
            cur->next = toDelete->next;
            if(toDelete->next)
                toDelete->next->prev = cur;
        }
    }
};
```

