# Get Minimum from the stack

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/get-minimum-element-from-stack/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Flipkart](../../company-based-lists/flipkart.md)
* [Walmart](../../company-based-lists/walmart.md)

### Problem Statement

You are given **N** elements and your task is to Implement a Stack in which you can get minimum element in O(1) time. You are required to complete the three methods **push()** which take one argument an integer **'x'** to be pushed into the stack, **pop()** which returns a integer poped out from the stack and **getMin()** which returns the min element from the stack. (-1 will be returned if for **pop() and getMin()** the stack is empty.)

**Example 1:**

```
Input:
push(2)
push(3)
pop()
getMin()
push(1)
getMin()
Output: 3 2 1
Explanation: In the first test case for
query 
push(2)  the stack will be {2}
push(3)  the stack will be {2 3}
pop()    poped element will be 3 the
         stack will be {2}
getMin() min element will be 2 
push(1)  the stack will be {2 1}
getMin() min element will be 1
```

**Expected Time Complexity** : O(1) for all the 3 methods.\
**Expected Auixilliary Space** : O(1) for all the 3 methods.

**Constraints:**\
&#x20;1 <= Number of queries <= 100\
&#x20;1 <= values of the stack <= 100

### Solution

_The trick would be to keep track of second minimum when we are removing(poping) the minimum from the stack. For that, while inserting a new minimum into the stack, instead of inserting the actual minimum we will insert `2*value - curr_minimum` . That way when we are poping the minimum, we can find the next minimum using `2*cur_minimum - value.`_

```cpp
/*
The structure of the class is as follows
class _stack{
stack<int> s;
int minEle;
public :
    int getMin();
    int pop();
    void push(int);
};
*/

/*returns min element from stack*/
int _stack :: getMin()
{
    if(this->s.empty())
        return -1;
    return this->minEle;
}

/*returns poped element from stack*/
int _stack ::pop()
{
    if(this->s.empty())
        return -1;
    
    int x = s.top(); s.pop();
    if(x >= this->minEle)
        return x;
    else
    {
       int prevMin  = (2 * this->minEle) - x;
       x = this->minEle;
       this->minEle = prevMin;
       return x;
    }
}

/*push element x into the stack*/
void _stack::push(int x)
{
    if(this->s.empty())
    {
        s.push(x);
        this->minEle = x;
        return;
    }
    if(x > this->minEle)
    {
        s.push(x);
    }
    else
    {
        int magic = (2 * x) - this->minEle;
        this->minEle = x;
        s.push(magic);
    }
}
```

