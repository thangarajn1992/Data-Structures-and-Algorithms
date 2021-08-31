# Find the peak element in an array first increases and then decreases

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/maximum-value-in-a-bitonic-array3001/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given an array **arr** of **n** elements which is first increasing and then may be decreasing, find the maximum element in the array. **Note:** If the array is increasing then just print then **last element** will be the maximum value.

**Example 1:**

```text
Input: 
n = 9
arr[] = {1,15,25,45,42,21,17,12,11}
Output: 45
Explanation: Maximum element is 45.
```

**Example 2:**

```text
Input: 
n = 5
arr[] = {1, 45, 47, 50, 5}
Output: 50
Explanation: Maximum element is 50.
```

**Expected Time Complexity:** O\(logn\)  
**Expected Auxiliary Space:** O\(1\)

**Constraints:**  
 3 ≤ n ≤ 10^6  
 1 ≤ arr\[i\] ≤ 10^6

### Solution

```cpp
class Solution{
public:
    int findMaximum(int arr[], int n) {
        int left = 0, right = n-1;
        while(left <= right)
        {
            int mid = (left + right) >> 1;
            if(arr[mid] > arr[mid-1] && arr[mid] > arr[mid+1]) // peak element
                return arr[mid];
            if(arr[mid] > arr[mid-1])
                left = mid + 1;
            else
                right = mid - 1;
        }
    }
};
```

