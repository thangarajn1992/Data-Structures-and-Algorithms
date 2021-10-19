# Rotate Array - Counter Clockwise

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/rotate-array-by-n-elements-1587115621/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given an unsorted array **arr\[]** of size **N**, rotate it by **D** elements in the counter-clockwise direction. The array must be modified in-place without using extra space.&#x20;

**Example 1:**

```
Input:
N = 5, D = 2
arr[] = {1,2,3,4,5}
Output: 3 4 5 1 2
Explanation: 1 2 3 4 5  when rotated
by 2 elements, it becomes 3 4 5 1 2.
```

**Example 2:**

```
Input:
N = 10, D = 3
arr[] = {2,4,6,8,10,12,14,16,18,20}
Output: 8 10 12 14 16 18 20 2 4 6
Explanation: 2 4 6 8 10 12 14 16 18 20 
when rotated by 3 elements, it becomes 
8 10 12 14 16 18 20 2 4 6.
```



**Expected Time Complexity: **O(N)\
&#x20;**Expected Auxiliary Space: **O(1)

**Constraints:**\
&#x20;1 <= N <= 10^7\
&#x20;1 <= D <= N\
&#x20;0 <= arr\[i] <= 10^5

### Solution

#### A Juggling Algorithm

Divide the array in different sets, where number of sets is equal to GCD of n and d and move the elements within sets. If GCD is 1 as is for this example array (n = 7 and d =2), then elements will be moved within one set only, we just start with temp = arr\[0] and keep moving arr\[I+d] to arr\[I] and finally store temp at the right place.

Here is an example for n =12 and d = 3. GCD is 3 and \
&#x20;

```
Let arr[] be {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12}

a) Elements are first moved in first set – (See below 
   diagram for this movement)
          arr[] after this step --> {4 2 3 7 5 6 10 8 9 1 11 12}

b)    Then in second set.
          arr[] after this step --> {4 5 3 7 8 6 10 11 9 1 2 12}

c)    Finally in third set.
          arr[] after this step --> {4 5 6 7 8 9 10 11 12 1 2 3}
```

```cpp
class Solution{
public:
    void rotateArr(int arr[], int d, int n){
        int start = 0, count = 0;
        while(count < n) // This loop will run GCD of(n,d) times
        {
            int curr = start;
            int prev = arr[curr];
            do
            {
               curr = (n - d + curr) % n;
               int temp = prev;
               prev = arr[curr];
               arr[curr] = temp;
               count++;
            }while(curr != start);
            start++;
        }
    }
};
```
