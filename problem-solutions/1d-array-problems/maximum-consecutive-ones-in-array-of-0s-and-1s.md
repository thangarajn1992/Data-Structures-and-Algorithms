# Maximum Consecutive Ones in array of 0s and 1s

### Sources

* [Leetcode 485](https://leetcode.com/problems/max-consecutive-ones/)

### Companies

### Problem Statement

Given a binary array `nums`, return _the maximum number of consecutive_ `1`_'s in the array_.

**Example 1:**

```text
Input: nums = [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s. 
The maximum number of consecutive 1s is 3.
```

**Example 2:**

```text
Input: nums = [1,0,1,1,0,1]
Output: 2
```

**Constraints:**

* `1 <= nums.length <= 10^5`
* `nums[i]` is either `0` or `1`.

### Solution

#### Sliding Window of variable length

```cpp
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int maxConsecutiveOnes = 0;
        int index = 0;
        int windowStart = -1; 
        // windowStart being -1 means we are not in the window of Ones
        for(; index < nums.size(); index++)
        {
            if(nums[index] == 0 && windowStart != -1) // end of window of Ones
            {
                maxConsecutiveOnes = max(maxConsecutiveOnes, index - windowStart);
                windowStart = -1;
            }
            else if(nums[index] == 1 && windowStart == -1) // Start of new window of Ones
                windowStart = index;
        }
        if(windowStart != -1) 
            maxConsecutiveOnes = max(maxConsecutiveOnes, index - windowStart);
        
        return maxConsecutiveOnes;
    }
};
```

