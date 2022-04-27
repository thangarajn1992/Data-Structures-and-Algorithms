# Maximum Rectangular Area in a Histogram

### Sources

* [GeeksForGeeks](https://practice.geeksforgeeks.org/problems/maximum-rectangular-area-in-a-histogram-1587115620/1#)
* [Leetcode 84](https://leetcode.com/problems/largest-rectangle-in-histogram/)

### Companies

* [Google](../../company-based-lists/google.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Find the largest rectangular area possible in a given histogram where the largest rectangle can be made of a number of contiguous bars. For simplicity, assume that all bars have the same width and the width is **1 unit**, there will be **N** bars height of each bar will be given by the array **arr**.

**Example 1:**

```
Input:
N = 7
arr[] = {6,2,5,4,5,1,6}
Output: 12
Explanation: 

```

![](<../../.gitbook/assets/image (57).png>)

**Example 2:**

```
Input:
N = 8
arr[] = {7 2 8 9 1 3 6 5}
Output: 16
Explanation: Maximum size of the histogram 
will be 8  and there will be 2 consecutive 
histogram. And hence the area of the 
histogram will be 8x2 = 16.
```

**Your Task:**\
The task is to complete the function **getMaxArea**() which takes the array arr\[] and its size N as inputs and finds the largest rectangular area possible and **returns** the answer.

**Expected Time Complxity** : O(N)\
**Expected Auxilliary Space** : O(N)

**Constraints:**\
1 ≤ N ≤ 10^6\
1 ≤ arr\[i] ≤ 10^12

### **Solution**

```cpp
class Solution
{
    public:
    //Function to find largest rectangular area possible in a given histogram.
    long long getMaxArea(long long arr[], int n)
    {
        stack<int> stk;
        long long int i = 0, max_a = 0;
        while (i < n) {
            if (stk.empty() || arr[i] >= arr[stk.top()]) 
                stk.push(i++);
            else {
                int h = stk.top();
                stk.pop();
                max_a = max(max_a, arr[h] * (stk.empty() ? i : i - stk.top() - 1));
            }
        }
        
        while(stk.empty() == false)
        {
            int h = stk.top();
            stk.pop();
            max_a = max(max_a, arr[h] * (stk.empty() ? n : n - stk.top() - 1));           
        }
        return max_a;       
    }
};
```
