# Search Insert Position

[Leetcode 35](https://leetcode.com/problems/search-insert-position/)

### Problem Statement

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

```text
Input: nums = [1,3,5,6], target = 5
Output: 2
```

**Example 2:**

```text
Input: nums = [1,3,5,6], target = 2
Output: 1
```

**Example 3:**

```text
Input: nums = [1,3,5,6], target = 7
Output: 4
```

**Example 4:**

```text
Input: nums = [1,3,5,6], target = 0
Output: 0
```

**Example 5:**

```text
Input: nums = [1], target = 0
Output: 0
```

**Constraints:**

* `1 <= nums.length <= 10^4`
* `-10^4 <= nums[i] <= 10^4`
* `nums` contains **distinct** values sorted in **ascending** order.
* `-10^4 <= target <= 10^4`

### Solution \( Basic Binary Search Algorithm\)

```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int left = 0, right = nums.size() - 1;
        while(left <= right)
        {
            int mid = left + (right - left)/2;
            if(nums[mid] == target)
                return mid;
            if(nums[mid] < target)
                left = mid+1;
            else
                right = mid-1;
        }
        return left;
    }
};
```

