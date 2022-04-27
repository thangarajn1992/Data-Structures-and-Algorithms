# Segregate even and odd nodes in a Link List

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/segregate-even-and-odd-nodes-in-a-linked-list5035/1#)

### Companies

### Problem Statement

Given a link list of size N, modify the list such that all the even numbers appear before all the odd numbers in the modified list. The order of appearance of numbers within each segregation should be same as that in the original list.

**NOTE:** Don't create a new linked list, instead rearrange the provided one.

\
**Example 1:**

```
Input: 
N = 7
Link List:
17 -> 15 -> 8 -> 9 -> 2 -> 4 -> 6 -> NULL

Output: 8 2 4 6 17 15 9

Explanation: 8,2,4,6 are the even numbers 
so they appear first and 17,15,9 are odd 
numbers that appear later.
```

\
**Example 2:**

```
Input:
N = 4
Link List:
1 -> 3 -> 5 -> 7

Output: 1 3 5 7

Explanation: There is no even number. 
So ne need for modification.
```

\
**Your Task:**\
You do not need to read input or print anything. Your task is to complete the function **divide()** which takes N and head of Link List as input parameters and returns the head of modified link list. Don't create a new linked list, instead rearrange the provided one.

\
**Expected Time Complexity:** O(N)\
**Expected Auxiliary Space:** O(1)

\
**Constraints:**\
1 ≤ N ≤ 10^5\
1 ≤ Each element of the list ≤ 10^5

### Solution

```cpp
class Solution{
public:
    Node* divide(int N, Node *head){
        Node *evendummy = new Node(0); 
        Node *odddummy = new Node(0);
        Node *evenHead = evendummy;
        Node *oddHead = odddummy, *curr = head;
        while(curr != nullptr)
        {
            if(curr->data % 2 == 0)
            {
                evenHead->next = curr;
                evenHead = evenHead->next;
            }
            else
            {
                oddHead->next = curr;
                oddHead = oddHead->next;
            }
            curr = curr->next;
        }
        
        evenHead->next = odddummy->next;
        oddHead->next = nullptr;
        return evendummy->next;
    }
};
```
