# All Unique Triplets that add upto to given sum

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/triplet-sum-in-array-1587115621/1#)
* [Leetcode 15](https://leetcode.com/problems/3sum/)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Samsung](../../company-based-lists/samsung.md)

### Problem Statement

Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

**Example 1:**

```text
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
```

**Example 2:**

```text
Input: nums = []
Output: []
```

**Example 3:**

```text
Input: nums = [0]
Output: []
```

**Constraints:**

* `0 <= nums.length <= 3000`
* `-10^5 <= nums[i] <= 10^5`

### Solution

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        if(nums.size() < 3)
            return {};
        vector<vector<int>> result;
        sort(nums.begin(), nums.end());
        for(int first = 0; first < nums.size() - 2; first++)
        {
            if(first > 0 && nums[first] == nums[first-1])
                continue;
            int second = first + 1;
            int third = nums.size() - 1;
            while(second < third)
            {
                int sum = nums[first] + nums[second] + nums[third];

                if(sum == 0)
                    result.push_back({nums[first], nums[second], nums[third]});
                if(sum > 0)
                {
                    third--;
                    while(second < third && nums[third] == nums[third+1])
                        third--;
                }
                else
                {
                    second++;
                    while(second < third && nums[second] == nums[second-1])
                        second++;
                }
            }
        }
        return result;
    }
};
```

