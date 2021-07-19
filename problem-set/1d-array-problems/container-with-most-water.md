# Container With Most Water

[Leetcode 11](https://leetcode.com/problems/container-with-most-water/)

### Problem Statement

Given `n` non-negative integers `a1, a2, ..., an` , where each represents a point at coordinate `(i, ai)`. `n` vertical lines are drawn such that the two endpoints of the line `i` is at `(i, ai)` and `(i, 0)`. Find two lines, which, together with the x-axis forms a container, such that the container contains the most water.

**Notice** that you may not slant the container.

**Example 1:** ![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

```text
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```

**Example 2:**

```text
Input: height = [1,1]
Output: 1
```

**Example 3:**

```text
Input: height = [4,3,2,1,4]
Output: 16
```

**Example 4:**

```text
Input: height = [1,2,1]
Output: 2
```

**Constraints:**

* `n == height.length`
* `2 <= n <= 10^5`
* `0 <= height[i] <= 10^4`

### Solution

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int left = 0, right = height.size() - 1;
        int max_area = 0;
        
        while(left <= right)
        {
            int cur_area = 0;
            if(height[left] <= height[right])
            {
                cur_area = height[left] * (right - left);
                left++;
            }
            else
            {
                cur_area = height[right] * (right - left);
                right--;
            }
            max_area = max(max_area, cur_area);
        }
        return max_area;
    }
};
```

