# Combination Sum - Input distinct Output Non-distinct subset Repeated Numbers

### Sources

* [Leetcode 377](https://leetcode.com/problems/combination-sum-iv/)

### Companies

### Problem Statement

Given an array of **distinct** integers `nums` and a target integer `target`, return _the number of possible combinations that add up to_ `target`.

The answer is **guaranteed** to fit in a **32-bit** integer.

**Example 1:**

```text
Input: nums = [1,2,3], target = 4
Output: 7
Explanation:
The possible combination ways are:
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)
Note that different sequences are counted as different combinations.
```

**Example 2:**

```text
Input: nums = [9], target = 3
Output: 0
```

**Constraints:**

* `1 <= nums.length <= 200`
* `1 <= nums[i] <= 1000`
* All the elements of `nums` are **unique**.
* `1 <= target <= 1000`

### Solution

```cpp
class Solution {
public:
    int combinationSum4(vector<int>& nums, int target) {
        vector<unsigned int> combos(target+1, 0);
        combos[0] = 1;
        for (int curTarget = 1; curTarget <= target; curTarget++)
        {
            for (int num : nums)
            {
                if (num <= curTarget) 
                    combos[curTarget] += combos[curTarget - num];
            }
        }
        return combos[target];
    }
};
```

