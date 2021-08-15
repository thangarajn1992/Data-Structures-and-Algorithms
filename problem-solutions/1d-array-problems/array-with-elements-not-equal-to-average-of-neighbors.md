# Array With Elements Not Equal to Average of Neighbors

### Source

* [Leetcode 1968](https://leetcode.com/problems/array-with-elements-not-equal-to-average-of-neighbors/)

### Problem Statement

You are given a **0-indexed** array `nums` of **distinct** integers. You want to rearrange the elements in the array such that every element in the rearranged array is **not** equal to the **average** of its neighbors.

More formally, the rearranged array should have the property such that for every `i` in the range `1 <= i < nums.length - 1`, `(nums[i-1] + nums[i+1]) / 2` is **not** equal to `nums[i]`.

Return _**any** rearrangement of_ `nums` _that meets the requirements_.

**Example 1:**

```text
Input: nums = [1,2,3,4,5]
Output: [1,2,4,5,3]
Explanation:
When i=1, nums[i] = 2, and the average of its neighbors is (1+4) / 2 = 2.5.
When i=2, nums[i] = 4, and the average of its neighbors is (2+5) / 2 = 3.5.
When i=3, nums[i] = 5, and the average of its neighbors is (4+3) / 2 = 3.5.
```

**Example 2:**

```text
Input: nums = [6,2,0,9,7]
Output: [9,7,6,2,0]
Explanation:
When i=1, nums[i] = 7, and the average of its neighbors is (9+6) / 2 = 7.5.
When i=2, nums[i] = 6, and the average of its neighbors is (7+2) / 2 = 4.5.
When i=3, nums[i] = 2, and the average of its neighbors is (6+0) / 2 = 3.
```

**Constraints:**

* `3 <= nums.length <= 10^5`
* `0 <= nums[i] <= 10^5`

### Solution

#### Two way scanning and swapping

* Scan from left to right and fix the invalid triplets by swapping
* Scan from right to left and fix the invalid triplets by swapping

```text
Example : {0, 1, 2, 3, 4, 5} -> Only doing 1st scan will fail here. So both scans is needed
```

```cpp
class Solution {
public:
    vector<int> rearrangeArray(vector<int>& nums) {
        int n = nums.size();
        
        // Move left to right and fix
        for (int i = 1; i < n - 1; i++) {

            if (2*nums[i] == (nums[i-1] + nums[i+1]))
                swap(nums[i], nums[i+1]);
        }
        
        // Move right to left and fix
        for (int i = nums.size() - 2; i > 0; i--) {

            if (2*nums[i] == (nums[i-1] + nums[i+1]))
                swap(nums[i], nums[i-1]);
        }
        return nums;   
    }
};
```

#### Sorting and Rearranging

If we make sure that `nums[i-1] < nums[i] > nums[i+1],` we are good to go. So, we can sort the input and choose wisely to satisfy above condition.

```text
Example : 
[6,2,0,9,7]
sort it : [0, 2, 6, 7, 9]
    
result  : [0, _, 2, _, 6] - 1st loop (fill alternaltely)
result  : [0, 7, 2, 9, 6] - 2nd loop (fill next larger numbers from nums to result in 
spaces left)
```

```cpp
class Solution {
public:
    vector<int> rearrangeArray(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        vector<int> answer(nums.size());
        int j = 0, i = 0;
        for(i = 0; j < nums.size(); i++, j+=2)
            answer[j] = nums[i];
        
        j = 1;
        for(; j < nums.size(); i++, j+=2)
            answer[j] = nums[i]
            
        return answer;
    }
};
```

