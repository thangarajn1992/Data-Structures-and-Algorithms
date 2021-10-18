# Sort a Stack

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/sort-a-stack/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given a stack, the task is to sort it such that the top of the stack has the greatest element.Your task is to complete the function **sort() **which sorts the elements present in the given stack.

**Example 1:**

```
Input:
Stack: 3 2 1
Output: 3 2 1
```

**Example 2:**

```
Input:
Stack: 11 2 32 3 41
Output: 41 32 11 3 2
```

**Expected Time Complexity**: O(N\*N)\
**Expected Auxiliary Space**: O(N) recursive.

**Constraints:**\
 1<= N <=100

### Solution

#### Iterative Approach

```cpp
void SortedStack :: sort()
{
    stack<int> order;
    while(s.empty() == false)
    {
        int element = s.top(); s.pop();
        while(order.empty() == false && order.top() > element)
        {
            s.push(order.top()); 
            order.pop();
        }
        order.push(element);
    }
    s = order;
}
```

#### Recursive Approach

```cpp
void SortedStack :: sort()
{
   if(s.size() == 1)
        return;
   int element = s.top(); s.pop();
   this->sort();
   stack<int> tmp;
   while(s.empty() == false && s.top() > element)
        tmp.push(s.top()), s.pop();
    s.push(element);
    while(tmp.empty() == false)
        s.push(tmp.top()), tmp.pop();
}
```
