# Intersection Point in Y Shaped Linked Lists

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/intersection-point-in-y-shapped-linked-lists/1#)
* [Leetcode 160](https://leetcode.com/problems/intersection-of-two-linked-lists/)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Flipkart](../../company-based-lists/flipkart.md)
* [Adobe](../../company-based-lists/adobe.md)

### Problem Statement

Given two singly linked lists of size **N** and **M,** write a program to get the point where two linked lists intersect each other.

**Example 1:**

![](../../.gitbook/assets/image%20%2837%29.png)

```text
Input:
LinkList1 = 3->6->9->common
LinkList2 = 10->common
common = 15->30->NULL
Output: 15
Explanation:

```

**Example 2:**

```text
Input: 
Linked List 1 = 4->1->common
Linked List 2 = 5->6->1->common
common = 8->4->5->NULL
Output: 8
Explanation: 

4              5
|              |
1              6
 \             /
  8   -----  1 
   |
   4
   |
  5
  |
  NULL       
```

**Your Task:**  
You don't need to read input or print anything. The task is to complete the function **intersetPoint**\(\) which takes the pointer to the head of linklist1\(**head1**\) and linklist2\(**head2**\) as input parameters and returns data value of a node where two linked lists intersect. If linked list do not merge at any point, then it should return **-1**.  
**Challenge** : Try to solve the problem without using any extra space.

**Expected Time Complexity:** O\(N+M\)  
**Expected Auxiliary Space:** O\(1\)

**Constraints:**  
 1 ≤ N + M ≤ 2\*10**^**5  
 -1000 ≤ value ≤ 1000

### Solution

#### Two Pointer Approach

```cpp
class Solution {
public:
    // curA starts from headA and once it reaches its end,then moves to headB
    // curB starts from headB and once it reaches its end,then moves to headA
    // If there is an intersection, they will meet at that node otherwise
    // they both endup traversing both lists once and meet at end (null).
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode *curA = headA, *curB = headB;
        while(curA != curB)
        {
            curA = curA ? curA->next : headB;
            curB = curB ? curB->next : headA;
        }
        return curA;
    }
};
```

#### Compute Lengths of both lists

```cpp
/* Linked List Node
struct Node {
  int data;
  struct Node *next;
  Node(int x) {
    data = x;
    next = NULL;
  }
}; */

//Function to find intersection point in Y shaped Linked Lists.
int intersectPoint(Node* head1, Node* head2)
{
    int list1Length = 0, list2Length = 0;
    Node *temp = nullptr;
    for(temp = head1; temp; temp = temp->next) 
        list1Length++;
    for(temp = head2; temp; temp = temp->next) 
        list2Length++;
    
    int diff = abs(list1Length - list2Length);
    
    if(list1Length > list2Length)
        while(diff--) 
            head1 = head1->next;
    else
        while(diff--) 
            head2 = head2->next;
        
    while(head1 != head2)
    {
        head1 = head1->next;
        head2 = head2->next;
    }
    return head1->data;
}
```

