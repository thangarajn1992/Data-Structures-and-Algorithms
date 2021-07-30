# Median of Two Sorted Arrays

[Leetcode 4](https://leetcode.com/problems/median-of-two-sorted-arrays/)

### Problem Statement

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return **the median** of the two sorted arrays.

The overall run time complexity should be `O(log (m+n))`.

**Example 1:**

```text
Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.
```

**Example 2:**

```text
Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
```

**Example 3:**

```text
Input: nums1 = [0,0], nums2 = [0,0]
Output: 0.00000
```

**Example 4:**

```text
Input: nums1 = [], nums2 = [1]
Output: 1.00000
```

**Example 5:**

```text
Input: nums1 = [2], nums2 = []
Output: 2.00000
```

**Constraints:**

* `nums1.length == m`
* `nums2.length == n`
* `0 <= m <= 1000`
* `0 <= n <= 1000`
* `1 <= m + n <= 2000`
* `-10^6 <= nums1[i], nums2[i] <= 10^6`

### Solution

```cpp
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int nums1_size = nums1.size();
        int nums2_size = nums2.size();
        int total_entry = nums1_size + nums2_size;
        
        // If we can just sort till the median index, it is enough
        int large_median_index = total_entry/2;
        vector<int> result(large_median_index + 1);
        
        int n1 = 0, n2 = 0, n3 = 0;
        while(n1 < nums1_size && n2 < nums2_size && n3 <= large_median_index)
        {
            if(nums1[n1] < nums2[n2])
                result[n3++] = nums1[n1++];
            else
                result[n3++] = nums2[n2++];
        }
        
        while(n1 < nums1_size && n3 <= large_median_index)
            result[n3++] = nums1[n1++];
        while(n2 < nums2_size && n3 <= large_median_index)
            result[n3++] = nums2[n2++];
        
        double median = 0;
        
        if(total_entry % 2 == 0)
            median = (double)(result.back() + result[result.size()-2]) / 2;
        else
            median = result.back();
        
        return median;
        
    }
};
```

