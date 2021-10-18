# Are Elements are within k distance from fully sorted array

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/k-sorted-array1610/1#)

### Companies

### Problem Statement

Given an array of **n** distinct elements. Check whether the given array is a **k** sorted array or not. A **k** sorted array is an array where each element is at most **k** distance away from its target position in the sorted array.

\
 **Example 1:**

```
Input:
N=6
arr[] = {3, 2, 1, 5, 6, 4} 
K = 2
Output: Yes
Explanation:
Every element is at most 2 distance 
away from its target position in the
sorted array.  
```

**Example 2:**

```
Input:
N=7
arr[] = {13, 8, 10, 7, 15, 14, 12}
K = 1
Output: No
```

**Expected Time Complexity:** O(NlogN).\
**Expected Auxiliary Space:** O(N).

**Constraints:**\
 1 ≤ N ≤ 10^5\
 0 ≤ K ≤ N

### Solution

#### Hash-Map Approach

```cpp
class Solution {
  public:
    string isKSortedArray(int arr[], int n, int k)
    {
        map<int,int> old_index;
        for(int i = 0; i < n; i++)
            old_index[arr[i]] = i;
            
        sort(arr, arr+n);
        
        for(int i = 0; i < n; i++)
            if(abs(i - old_index[arr[i]]) > k)
                return "No";
      
        return "Yes";
    }
};
```

#### Binary Search Approach

```cpp
class Solution {
  public:
    string isKSortedArray(int arr[], int n, int k)
    {
        int sortedArray[n];
        for(int index = 0; index < n; index++)
            sortedArray[index] = arr[index];
            
        sort(sortedArray, sortedArray+n);
        
        for(int index = 0; index < n; index++)
        {
            int pos = binarySearch(sortedArray, n, arr[index]);
            if(abs(index - pos) > k)
                return "No";    
        }
        return "Yes";
    }
    
    int binarySearch(int sortedArray[], int n, int value)
    {
        int left = 0, right = n-1;
        while(left < right)
        {
            int mid = left + (right - left)/2;
            if(sortedArray[mid] == value)
                return mid;
            else if(sortedArray[mid] < value)
                left = mid+1;
            else
                right = mid-1;
        }
        return left;
    }
```
