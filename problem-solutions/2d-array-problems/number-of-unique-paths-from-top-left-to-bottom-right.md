# Number of Unique Paths from Top Left to Bottom Right

### Sources

* [Leetcode 62](https://leetcode.com/problems/unique-paths/)
* [GeeksForGeeks](https://practice.geeksforgeeks.org/problems/number-of-unique-paths5339/1#)

### Companies

* [Walmart](../../company-based-lists/walmart.md)

### Problem Statement

A robot is located at the top-left corner of a `m x n` grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/22/robot\_maze.png)

```
Input: m = 3, n = 7
Output: 28
```

**Example 2:**

```
Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down
2. Down -> Down -> Right
3. Down -> Right -> Down
```

**Example 3:**

```
Input: m = 7, n = 3
Output: 28
```

**Example 4:**

```
Input: m = 3, n = 3
Output: 6
```

**Constraints:**

* `1 <= m, n <= 100`
* It's guaranteed that the answer will be less than or equal to `2 * 10^9`.

### Solution

```cpp
class Solution {
public:
    int uniquePaths(int rows, int cols) {
        vector<int> paths(cols, 1);
        // For first row everything is 1, so we initialized dp vector with all 1s
        for(int row = 1; row < rows; row++)
        {
            // for first col it is always 1, so we run loop from second column
            // paths[col] is above cell and paths[col-1] is left cell.
            // new paths[col] = paths[col] + paths[col-1];
            for(int col = 1; col < cols; col++)
                paths[col] = paths[col] + paths[col-1];
        }
        return paths[cols-1];
    }
};
```
