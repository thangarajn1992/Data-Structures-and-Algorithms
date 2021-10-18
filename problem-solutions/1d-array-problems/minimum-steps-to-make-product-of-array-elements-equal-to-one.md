# Minimum steps to make product of array elements equal to one

### Source

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/minimum-steps-to-make-product-equal-to-one/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given an array **arr\[]** containing **N** integers. In one step, any element of the array can either be increased or decreased by one. Find minimum steps required such that the product of the array elements becomes **1**.

**Example 1:**

```
Input:
N = 3
arr[] = {-2, 4, 0}
Output:
5
Explanation:
We can change -2 to -1, 0 to -1 and 4 to 1.
So, a total of 5 steps are required
to update the elements such that
the product of the final array is 1. 
```

**Example 2:**

```
Input:
N = 3
arr[] = {-1, 1, -1} 
Output :
0
Explanation:
Product of the array is already 1.
So, we don't need to change anything.
```

\
 **Your Task:  **\
 You don't need to read input or print anything. Your task is to complete the function **makeProductOne()** which takes an integer N and an array arr of size N as input and returns the minimum steps required.

\
 **Expected Time Complexity:** O(N)\
 **Expected Auxiliary Space:** O(1)

\
 **Constraints:**\
 1 ≤ N ≤ 10^5\
 \-10^3 ≤ arr\[i] ≤ 10^3

### Solution

#### Approach:

1. Move all negative numbers to -1, since they are closer to -1 than to 1.
2. Similarly move all positive numbers to +1, since they are closer +1 than to -1.
3. Keep the count of -1s and 0s.
4. If number of -1s is odd
   1. Compensate it by moving one of the zeroes to -1 instead of 1.  Moving 0 to 1 or -1 is same step count.
   2. If Zeroes are not available, then add 2 to step count ( moving that odd -1 to 1 takes 2 steps).

```cpp
class Solution {
  public:
    int makeProductOne(int arr[], int N) {
        int step_count = 0;
        int sign_count = 0;
        int zero_count = 0;
        for(int i = 0; i < N; i++)
        {
            if(arr[i] == 0) // Zero
            {
                zero_count++;
                step_count++;
            }
            else if(arr[i] < 0) // Negative 
            {
                step_count += -1 - arr[i];
                sign_count++;
            }
            else // Positive
            {
                step_count += arr[i] - 1;
            }
        }
        // If there are odd number of negatives, then try to compensate with 0 to -1
        // If Zero is there, no change in count
        // If Zero is not there, move one -1 to 1, increment step count by 2.
        if(sign_count % 2)
            step_count += (zero_count)? 0 : 2;
        
        return step_count;
    }
};
```
