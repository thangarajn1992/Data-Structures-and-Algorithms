# Product of every other element except the current element

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/product-array-puzzle4525/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given an array **nums\[]** of size **n**, construct a Product Array **P** (of same size n) such that **P\[i]** is equal to the product of all the elements of **nums** except nums\[i]. If the array has only one element the returned list should should contains one value i.e {1}\
&#x20;**Note:** Try to solve this problem without using the division operation

**Example 1:**

```
Input:
n = 5
nums[] = {10, 3, 5, 6, 2}
Output:
180 600 360 300 900
Explanation: 
For i=0, P[i] = 3*5*6*2 = 180.
For i=1, P[i] = 10*5*6*2 = 600.
For i=2, P[i] = 10*3*6*2 = 360.
For i=3, P[i] = 10*3*5*2 = 300.
For i=4, P[i] = 10*3*5*6 = 900.
```

**Example 2:**

```
Input:
n = 2
nums[] = {12,0}
Output:
0 12

```

**Expected Time Complexity:** O(n)\
**Expected Auxiliary Space:** O(n)\
&#x20;&#x20;

**Constraints:**\
&#x20;1 <= n <= 1000\
&#x20;0 <= nums\[i] <= 200\
&#x20;Array may contain duplicates.

### Solution

```cpp
class Solution{
  public:
    vector<long long int> productExceptSelf(vector<long long int>& nums, int n) {
       vector<long long int> result(n);
       long long int temp = 1;
       for(int i = 0; i < nums.size(); i++)
       {
          result[i] = temp;
          temp *= nums[i];
       }
       temp = 1;
       for(int i = nums.size()-1; i >= 0 ; i--)
       {
          result[i] *= temp;
          temp *= nums[i];
       }
       return result;
    }
};
```
