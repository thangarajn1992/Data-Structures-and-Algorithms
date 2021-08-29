# How many numbers to be patched into array to make all numbers from \[1,n\]

### Sources

* [Leetcode 330](https://leetcode.com/problems/patching-array/)

### Companies

### Problem Statement

Given a sorted integer array `nums` and an integer `n`, add/patch elements to the array such that any number in the range `[1, n]` inclusive can be formed by the sum of some elements in the array.

Return _the minimum number of patches required_.

**Example 1:**

```text
Input: nums = [1,3], n = 6
Output: 1
Explanation:
Combinations of nums are [1], [3], [1,3], which form possible sums of: 1, 3, 4.
Now if we add/patch 2 to nums, the combinations are: [1], [2], [3], [1,3], [2,3], [1,2,3].
Possible sums are 1, 2, 3, 4, 5, 6, which now covers the range [1, 6].
So we only need 1 patch.
```

**Example 2:**

```text
Input: nums = [1,5,10], n = 20
Output: 2
Explanation: The two patches can be [2, 4].
```

**Example 3:**

```text
Input: nums = [1,2,2], n = 5
Output: 0
```

**Constraints:**

* `1 <= nums.length <= 1000`
* `1 <= nums[i] <= 10^4`
* `nums` is sorted in **ascending order**.
* `1 <= n <= 2^31 - 1`

### Solution

```cpp
class Solution {
public:
    int minPatches(vector<int>& nums, int n) { 
        /*
        Let say, Count be the number that maximum number that can be formed so far + 1;
        As we traverse through the nums, we see compare our element and count value
        If element <= count, then we can reach count + element now so count += element
        else, we need to add "count" into our nums, count += count;
        */
        int patches = 0;
        int count = 1; 
        int i = 0;
        int size = nums.size();
        while (count <= n) {
            if (i < size && nums[i] <= count) 
            {
                count += nums[i];
                i++;
            }
            else {
                count += count;
                patches++;
            }
        }
        return patches;
    }
};
```

