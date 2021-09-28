# Rearrange array elements such that even elements are at even index and odd at odd index

### Sources

* [Leetcode 922](https://leetcode.com/problems/sort-array-by-parity-ii/)

### Companies

### Problem Statement

Given an array of integers `nums`, half of the integers in `nums` are **odd**, and the other half are **even**.

Sort the array so that whenever `nums[i]` is odd, `i` is **odd**, and whenever `nums[i]` is even, `i` is **even**.

Return _any answer array that satisfies this condition_.

**Example 1:**

```text
Input: nums = [4,2,5,7]
Output: [4,5,2,7]
Explanation: [4,7,2,5], [2,5,4,7], [2,7,4,5] would also have been accepted.
```

**Example 2:**

```text
Input: nums = [2,3]
Output: [2,3]
```

**Constraints:**

* `2 <= nums.length <= 2 * 10^4`
* `nums.length` is even.
* Half of the integers in `nums` are even.
* `0 <= nums[i] <= 1000`

**Follow Up:** Could you solve it in-place?

### Solution

```cpp
// Find the odd and even index that misplaced and swap them
class Solution {
public:
    vector<int> sortArrayByParityII(vector<int>& nums) {
        for (int evenIndex = 0, oddIndex = 1; 
             evenIndex < nums.size(); 
             evenIndex += 2, oddIndex += 2) {
            while (evenIndex < nums.size() && nums[evenIndex] % 2 == 0) 
                evenIndex += 2;
            while (oddIndex < nums.size() && nums[oddIndex] % 2 == 1) 
                oddIndex += 2;
            if (evenIndex < nums.size()) 
                swap(nums[evenIndex], nums[oddIndex]);
        }
        return nums;
    }
};
```

