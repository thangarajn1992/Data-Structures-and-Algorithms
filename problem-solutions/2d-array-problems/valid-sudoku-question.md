# Valid Sudoku Question

### Source

* [Leetcode 36](https://leetcode.com/problems/valid-sudoku/)

### Companies



### Problem Statement

Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the nine `3 x 3` sub-boxes of the grid must contain the digits `1-9` without repetition.

**Note:**

* A Sudoku board \(partially filled\) could be valid but is not necessarily solvable.
* Only the filled cells need to be validated according to the mentioned rules.

**Example 1:** 

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

```text
Input: board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
```

**Example 2:**

```text
Input: board = 
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

**Constraints:**

* `board.length == 9`
* `board[i].length == 9`
* `board[i][j]` is a digit or `'.'`.

### Solution

```cpp
#define BOARD_SIZE 9
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        bool rows[BOARD_SIZE][BOARD_SIZE] = {false};
        bool cols[BOARD_SIZE][BOARD_SIZE] = {false};
        bool boxs[BOARD_SIZE][BOARD_SIZE] = {false};
        for(int row = 0; row < BOARD_SIZE; row++)
            for(int col = 0; col < BOARD_SIZE; col++)
                if(board[row][col] != '.') {  
                    int num = board[row][col] - '1';  
                    int box = (row / 3) * 3 + col / 3;
                    if(rows[row][num] || cols[col][num] || boxs[box][num]) 
                        return false;
                    rows[row][num] = cols[col][num] = boxs[box][num] = true;
                }
        return true;
    }
};
```

