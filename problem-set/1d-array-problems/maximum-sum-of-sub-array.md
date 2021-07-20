# Maximum Sum of Sub-Array

[Leetcode 53](https://leetcode.com/problems/maximum-subarray/)   

[InterviewBit](https://www.interviewbit.com/problems/max-sum-contiguous-subarray/)

### Problem Statement

Given an integer array `nums`, find the contiguous subarray \(containing at least one number\) which has the largest sum and return _its sum_.

**Example 1:**

```text
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

**Example 2:**

```text
Input: nums = [1]
Output: 1
```

**Example 3:**

```text
Input: nums = [5,4,-1,7,8]
Output: 23
```

**Constraints:**

* `1 <= nums.length <= 3 * 10^4`
* `-10^5 <= nums[i] <= 10^5`

  **Follow up:** If you have figured out the `O(n)` solution, try coding another solution using the **divide and conquer** approach, which is more subtle.            

### Solution

#### O\(n\) Time Complexity

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int max_so_far = 0, maxi = INT_MIN;
        int size = nums.size();
        for(int &num : nums)
        {
            max_so_far = max(max_so_far + num, num);
            maxi = max(maxi, max_so_far);
        }
        return maxi;
    }
};
```

