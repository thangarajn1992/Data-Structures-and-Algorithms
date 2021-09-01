# Array Nesting

### Sources

* [Leetcode 565](https://leetcode.com/problems/array-nesting/)

### Companies

### Problem Statement

You are given an integer array `nums` of length `n` where `nums` is a permutation of the numbers in the range `[0, n - 1]`.

You should build a set `s[k] = {nums[k], nums[nums[k]], nums[nums[nums[k]]], ... }` subjected to the following rule:

* The first element in `s[k]` starts with the selection of the element `nums[k]` of `index = k`.
* The next element in `s[k]` should be `nums[nums[k]]`, and then `nums[nums[nums[k]]]`, and so on.
* We stop adding right before a duplicate element occurs in `s[k]`.

Return _the longest length of a set_ `s[k]`.

**Example 1:**

```text
Input: nums = [5,4,0,3,1,6,2]
Output: 4
Explanation: 
nums[0] = 5, nums[1] = 4, nums[2] = 0, nums[3] = 3, nums[4] = 1, nums[5] = 6, nums[6] = 2.
One of the longest sets s[k]:
s[0] = {nums[0], nums[5], nums[6], nums[2]} = {5, 6, 2, 0}
```

**Example 2:**

```text
Input: nums = [0,1,2]
Output: 1
```

**Constraints:**

* `1 <= nums.length <= 10^5`
* `0 <= nums[i] < nums.length`
* All the values of `nums` are **unique**.

### Solution

The entire range can be divided into set of elements with cyclic dependencies. No element outside any cycle could lead to an element inside the cycle. So we just need to process each cycle once \(by changing the array element visited to -1\) and find the cycle with maximum elements.

```cpp
class Solution {
public:
    int arrayNesting(vector<int>& nums) {
        int maxNestLength = 0;
        int size = nums.size();
        for(int index = 0; index < size; index++)
        {
            if(nums[index] != -1)
            {
                int start = index, curNestLength = 0;
                while(nums[start] != -1)
                {
                    curNestLength++;
                    int temp = start;
                    start = nums[start];
                    nums[temp] = -1;
                }
                if(curNestLength > maxNestLength)
                    maxNestLength = curNestLength;
            }
        }
        return maxNestLength;
    }
};
```

