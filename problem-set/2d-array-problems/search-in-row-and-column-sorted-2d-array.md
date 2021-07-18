# Search in Row and Column Sorted 2D Array

[Leetcode 240](https://leetcode.com/problems/search-a-2d-matrix-ii/)

### Problem Statement

Write an efficient algorithm that searches for a `target` value in an `m x n` integer `matrix`. The `matrix` has the following properties:

* Integers in each row are sorted in ascending from left to right.
* Integers in each column are sorted in ascending from top to bottom.

**Example 1:** ![](https://assets.leetcode.com/uploads/2020/11/24/searchgrid2.jpg)

```text
Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 5
Output: true
```

**Example 2:** ![](https://assets.leetcode.com/uploads/2020/11/24/searchgrid.jpg)

```text
Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 20
Output: false
```

**Constraints:**

* `m == matrix.length`
* `n == matrix[i].length`
* `1 <= n, m <= 300`
* `-10^9 <= matix[i][j] <= 10^9`
* All the integers in each row are **sorted** in ascending order.
* All the integers in each column are **sorted** in ascending order.
* `-10^9 <= target <= 10^9`

### Solution

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int rows = matrix.size();
        int row = 0;
        int col = matrix[0].size()-1;
        while(row < rows && col >= 0)
        {
            if(matrix[row][col] == target)
                return true;
            if(matrix[row][col] < target)
                row++;
            else
                col--;
        }
        return false;
    }       
};
```

