# Find the middle index with left sum equal to right sum

### Sources

* [Leetcode 1991](https://leetcode.com/problems/find-the-middle-index-in-array/)

### Companies

### Problem Statement

Given a **0-indexed** integer array `nums`, find the **leftmost** `middleIndex` \(i.e., the smallest amongst all the possible ones\).

A `middleIndex` is an index where `nums[0] + nums[1] + ... + nums[middleIndex-1] == nums[middleIndex+1] + nums[middleIndex+2] + ... + nums[nums.length-1]`.

If `middleIndex == 0`, the left side sum is considered to be `0`. Similarly, if `middleIndex == nums.length - 1`, the right side sum is considered to be `0`.

Return _the **leftmost**_ `middleIndex` _that satisfies the condition, or_ `-1` _if there is no such index_.

**Example 1:**

```text
Input: nums = [2,3,-1,8,4]
Output: 3
Explanation:
The sum of the numbers before index 3 is: 2 + 3 + -1 = 4
The sum of the numbers after index 3 is: 4 = 4
```

**Example 2:**

```text
Input: nums = [1,-1,4]
Output: 2
Explanation:
The sum of the numbers before index 2 is: 1 + -1 = 0
The sum of the numbers after index 2 is: 0
```

**Example 3:**

```text
Input: nums = [2,5]
Output: -1
Explanation:
There is no valid middleIndex.
```

**Example 4:**

```text
Input: nums = [1]
Output: 0
Explantion:
The sum of the numbers before index 0 is: 0
The sum of the numbers after index 0 is: 0
```

**Constraints:**

* `1 <= nums.length <= 100`
* `-1000 <= nums[i] <= 1000`

### Solution

```cpp
class Solution {
public:
    int findMiddleIndex(vector<int>& nums) {
        int size = nums.size();
        vector<int> fwdSum(size+1,0);
        
        for(int index = 1; index <= size; index++)
            fwdSum[index] = fwdSum[index-1] + nums[index-1];
        
        for(int index = 0; index < size; index++)
            if(fwdSum[index] == fwdSum[size] - fwdSum[index+1])
                return index;
    
        return -1;
    }
};
```

