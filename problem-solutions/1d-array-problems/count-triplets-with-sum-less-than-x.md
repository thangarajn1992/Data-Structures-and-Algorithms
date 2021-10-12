# Count Triplets with sum less than X

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/count-triplets-with-sum-smaller-than-x5549/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)

### Problem Statement

Given an array **arr\[]** of distinct integers of size **N** and a value **sum**, the task is to find the count of triplets **(i, j, k)**, having **(i\<j\<k) **with the sum of** (arr\[i] + arr\[j] + arr\[k]) **smaller than the given value sum.

\
**Example 1:**

```
Input: N = 4, sum = 2
arr[] = {-2, 0, 1, 3}
Output:  2
Explanation: Below are triplets with 
sum less than 2 (-2, 0, 1) and (-2, 0, 3). 
```

 

**Example 2:**

```
Input: N = 5, sum = 12
arr[] = {5, 1, 3, 4, 7}
Output: 4
Explanation: Below are triplets with 
sum less than 12 (1, 3, 4), (1, 3, 5), 
(1, 3, 7) and (1, 4, 5).
```

\
**Expected Time Complexity: **O(N^2).\
**Expected Auxiliary Space: **O(1).

\
**Constraints:**\
3 ≤ N ≤ 10^3

\-10^3 ≤ arr\[i] ≤ 10^3

### Solution

```cpp
class Solution{
	public:
	long long countTriplets(long long arr[], int n, long long sum)
	{
	    long long int triplets  = 0;
	    sort(arr, arr+n);
	    for(int index = 0; index < n-2; index++)
	    {
	        int left = index+1, right = n-1;
	        while(left < right)
	        {
	            int curSum = arr[index] + arr[left] + arr[right];
	            if(curSum >= sum)
	                right--;
	            else
	            {
	                triplets += (right - left);
	                left++;
	            }
	        }
	    }
	    return triplets;
	}
};
```
