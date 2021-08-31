# Find Minimum in Rotated Sorted Array with duplicates

### Sources

* [Leetcode 154](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/)

### Companies

### Problem Statement

Suppose an array of length `n` sorted in ascending order is **rotated** between `1` and `n` times. For example, the array `nums = [0,1,4,4,5,6,7]` might become:

* `[4,5,6,7,0,1,4]` if it was rotated `4` times.
* `[0,1,4,4,5,6,7]` if it was rotated `7` times.

Notice that **rotating** an array `[a[0], a[1], a[2], ..., a[n-1]]` 1 time results in the array `[a[n-1], a[0], a[1], a[2], ..., a[n-2]]`.

Given the sorted rotated array `nums` that may contain **duplicates**, return _the minimum element of this array_.

You must decrease the overall operation steps as much as possible.

**Example 1:**

```text
Input: nums = [1,3,5]
Output: 1
```

**Example 2:**

```text
Input: nums = [2,2,2,0,1]
Output: 0
```

**Constraints:**

* `n == nums.length`
* `1 <= n <= 5000`
* `-5000 <= nums[i] <= 5000`
* `nums` is sorted and rotated between `1` and `n` times.

### Solution

#### Binary Search Approach

```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        int left = 0, right = nums.size()-1;
        while(left < right)
        {
            int mid = (left + right) >> 1;
            if(nums[mid] < nums[right])
                right = mid;
            else if(nums[mid] > nums[right])
                left = mid + 1;
            else
                right--;
        }
        return nums[left];
    }
};
```

