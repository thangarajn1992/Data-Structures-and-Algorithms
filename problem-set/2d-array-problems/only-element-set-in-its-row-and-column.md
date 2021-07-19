# Only Element Set in its Row & Column

[Leetcode 1582](https://leetcode.com/problems/special-positions-in-a-binary-matrix/)

### Problem Statement

Given a `rows x cols` matrix `mat`, where `mat[i][j]` is either `0` or `1`, return _the number of special positions in `mat`._

A position `(i,j)` is called **special** if `mat[i][j] == 1` and all other elements in row `i` and column `j` are `0` \(rows and columns are **0-indexed**\).

**Example 1:**

```text
Input: mat = [[1,0,0],
              [0,0,1],
              [1,0,0]]
Output: 1
Explanation: 
(1,2) is a special position because mat[1][2] == 1 and all other elements in row 1 and 
column 2 are 0.
```

**Example 2:**

```text
Input: mat = [[1,0,0],
              [0,1,0],
              [0,0,1]]
Output: 3
Explanation: (0,0), (1,1) and (2,2) are special positions. 
```

**Example 3:**

```text
Input: mat = [[0,0,0,1],
              [1,0,0,0],
              [0,1,1,0],
              [0,0,0,0]]
Output: 2
```

**Example 4:**

```text
Input: mat = [[0,0,0,0,0],
              [1,0,0,0,0],
              [0,1,0,0,0],
              [0,0,1,0,0],
              [0,0,0,1,1]]
Output: 3
```

**Constraints:**

* `rows == mat.length`
* `cols == mat[i].length`
* `1 <= rows, cols <= 100`
* `mat[i][j]` is `0` or `1`.

### Solution

```cpp
class Solution {
public:
    int numSpecial(vector<vector<int>>& mat) {
        int rows = mat.size();
        int cols = mat[0].size();
        int special = 0;
        
        vector<int> row_ones_count(rows,0);
        vector<int> col_ones_count(cols,0);
        
        for(int row = 0; row < rows; row++)
            for(int col = 0; col < cols; col++)
                if(mat[row][col])
                    row_ones_count[row]++, col_ones_count[col]++;
        
        for(int row = 0; row < rows; row++)
            for(int col = 0; col < cols; col++)
                if(mat[row][col] && row_ones_count[row] == 1 && col_ones_count[col] == 1)
                    special++;
        
        return special;
    }
};
```

