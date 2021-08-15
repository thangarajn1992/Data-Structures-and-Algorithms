# Last Day Where You Can Still Cross

### Source

* [Leetcode 1970](https://leetcode.com/problems/last-day-where-you-can-still-cross/)

### Problem Statement

There is a **1-based** binary matrix where `0` represents land and `1` represents water. You are given integers `row` and `col` representing the number of rows and columns in the matrix, respectively.

Initially on day `0`, the **entire** matrix is **land**. However, each day a new cell becomes flooded with **water**. You are given a **1-based** 2D array `cells`, where `cells[i] = [ri, ci]` represents that on the `ith` day, the cell on the `rith` row and `cith` column \(**1-based** coordinates\) will be covered with **water** \(i.e., changed to `1`\).

You want to find the **last** day that it is possible to walk from the **top** to the **bottom** by only walking on land cells. You can start from **any** cell in the top row and end at **any** cell in the bottom row. You can only travel in the **four** cardinal directions \(left, right, up, and down\).

Return _the **last** day where it is possible to walk from the **top** to the **bottom** by only walking on land cells_.

**Example 1:** 

![](https://assets.leetcode.com/uploads/2021/07/27/1.png)

```text
Input: row = 2, col = 2, cells = [[1,1],[2,1],[1,2],[2,2]]
Output: 2
Explanation: The above image depicts how the matrix changes each day starting from day 0.
The last day where it is possible to cross from top to bottom is on day 2.
```

**Example 2:** 

![](https://assets.leetcode.com/uploads/2021/07/27/2.png)

```text
Input: row = 2, col = 2, cells = [[1,1],[1,2],[2,1],[2,2]]
Output: 1
Explanation: The above image depicts how the matrix changes each day starting from day 0.
The last day where it is possible to cross from top to bottom is on day 1.
```

**Example 3:** 

![](https://assets.leetcode.com/uploads/2021/07/27/3.png)

```text
Input: row = 3, col = 3, cells = [[1,2],[2,1],[3,3],[2,2],[1,1],[1,3],[2,3],[3,2],[3,1]]
Output: 3
Explanation: The above image depicts how the matrix changes each day starting from day 0.
The last day where it is possible to cross from top to bottom is on day 3.
```

**Constraints:**

* `2 <= row, col <= 2 * 10^4`
* `4 <= row * col <= 2 * 10^4`
* `cells.length == row * col`
* `1 <= ri <= row`
* `1 <= ci <= col`
* All the values of `cells` are **unique**.

### Solution

#### Graph DFS + Binary Search

```cpp
class Solution {
    public:
    int latestDayToCross(int row, int col, vector<vector<int>>& cells) {
        int left = 0, right = cells.size()-1;
        while(left <= right)
        {
            int mid = left + (right - left)/2;
            // Populate the grid at the "mid" day
            vector<vector<int>> grid(row+1, vector<int>(col+1,0));
            for(int i = 0; i <= mid; i++)
                grid[cells[i][0]][cells[i][1]] = 1; 
            
            bool reachable = false;
            // check reachability of any entry in last row from any of the first row entry
            for(int i = 1; i <= col; i++)
            {
                
                if(grid[1][i] == 0)
                {
                    vector<vector<bool>> visited(row+1, vector<bool>(col+1, false));
                    if(dfs(grid, 1, i, visited))
                    {
                        reachable = true;
                        break;
                    }   
                }
            }
            if(reachable)
                left = mid+1;
            else
                right = mid-1;
            
        }
        return left;
    }
    
    bool dfs(vector<vector<int>>&grid, int r, int c, vector<vector<bool>>& visited) {
 
        if(r >= grid.size() || c >= grid[0].size() || r <= 0 || c <= 0 || grid[r][c] == 1 || visited[r][c]) {
            return false;
        }
        if(r == grid.size()-1) {
            return true;
        }
        visited[r][c] = true;
        if(dfs(grid, r+1, c, visited))  {
            return true;
        }
        if(dfs(grid, r, c+1, visited))  {
            return true;
        }
        if(dfs(grid, r-1, c, visited)) {
            return true;
        }
        return dfs(grid, r, c-1, visited);
    }
};
```

