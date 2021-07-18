# Search in 2D Array

[Leetcode 74](https://leetcode.com/problems/search-a-2d-matrix/)

### Problem Statement

Write an efficient algorithm that searches for a value in an `m x n` matrix. This matrix has the following properties:

* Integers in each row are sorted from left to right.
* The first integer of each row is greater than the last integer of the previous row.

**Example 1:** ![](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)

```text
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
```

**Example 2:** ![](https://assets.leetcode.com/uploads/2020/10/05/mat2.jpg)

```text
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
Output: false
```

**Constraints:**

* `m == matrix.length`
* `n == matrix[i].length`
* `1 <= m, n <= 100`
* `-10^4 <= matrix[i][j], target <= 10^4`

### Solution

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int rows = matrix.size();
        int cols = matrix[0].size();
        
        int low = 0, high = rows*cols - 1;
        while(low <= high)
        {
            int mid = low + (high - low)/2;
            int r = mid/cols;
            int c = mid%cols;
            if(matrix[r][c] == target)
                return true;
            else if(matrix[r][c] < target)
                low = mid + 1;
            else
                high = mid - 1;
        }
        return false;
    }
};
```

