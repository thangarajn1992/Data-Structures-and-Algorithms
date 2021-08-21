# Sudoku Solver

### Sources

* [Leetcode 37](https://leetcode.com/problems/sudoku-solver/)

### Companies

### Problem Statement

Write a program to solve a Sudoku puzzle by filling the empty cells.

A sudoku solution must satisfy **all of the following rules**:

1. Each of the digits `1-9` must occur exactly once in each row.
2. Each of the digits `1-9` must occur exactly once in each column.
3. Each of the digits `1-9` must occur exactly once in each of the 9 `3x3` sub-boxes of the grid.

The `'.'` character indicates empty cells.

Example 1:

 

![](../../.gitbook/assets/image%20%2825%29.png)

```text
Input: board = [["5","3",".",".","7",".",".",".","."],["6",".",".","1","9","5",".",".","."],[".","9","8",".",".",".",".","6","."],["8",".",".",".","6",".",".",".","3"],["4",".",".","8",".","3",".",".","1"],["7",".",".",".","2",".",".",".","6"],[".","6",".",".",".",".","2","8","."],[".",".",".","4","1","9",".",".","5"],[".",".",".",".","8",".",".","7","9"]]
Output: [["5","3","4","6","7","8","9","1","2"],["6","7","2","1","9","5","3","4","8"],["1","9","8","3","4","2","5","6","7"],["8","5","9","7","6","1","4","2","3"],["4","2","6","8","5","3","7","9","1"],["7","1","3","9","2","4","8","5","6"],["9","6","1","5","3","7","2","8","4"],["2","8","7","4","1","9","6","3","5"],["3","4","5","2","8","6","1","7","9"]]
Explanation: The input board is shown above and the only valid solution is shown below:
```

![](../../.gitbook/assets/image%20%2826%29.png)



**Constraints:**

* `board.length == 9`
* `board[i].length == 9`
* `board[i][j]` is a digit or `'.'`.
* It is **guaranteed** that the input board has only one solution.

### Solution

#### Backtracking + Bool vector

```cpp
class Solution {
public:
    vector<vector<bool>> rows;
    vector<vector<bool>> cols;
    vector<vector<bool>> boxs;
    vector<vector<int>> emptyCells;
    
    void solveSudoku(vector<vector<char>>& board) {
        rows.resize(9, vector<bool>(9,false));
        cols.resize(9, vector<bool>(9,false));
        boxs.resize(9, vector<bool>(9,false));
        
        //Set prefilled nums and populate empty cells to be filled

        for(int row = 0; row < 9; row++)
        {
            for(int col = 0; col < 9; col++)
            {
                if(board[row][col] != '.')
                {
                    int num = board[row][col] - '1';
                    int box = 3*(row/3) + (col/3);
                    rows[row][num] = cols[col][num] = boxs[box][num] = true;
                }
                else
                {
                    emptyCells.push_back({row,col}); 
                }
            }
        }
        solver(board, 0);
    }
    
    bool solver(vector<vector<char>>&board, int index)
    {
   
        if(index == emptyCells.size())
            return true;
        
        int row = emptyCells[index][0], col = emptyCells[index][1];
        int box = 3*(row/3) + (col/3);
        
        for(int num = 0; num < 9; num++)
        {
            if(rows[row][num] == false && cols[col][num] == false &&
                boxs[box][num] == false)
            {
                board[row][col] = num + '1';
                rows[row][num] = cols[col][num] = boxs[box][num] = true;
                
                if(solver(board, index+1))
                    return true;
                
                board[row][col] = '.';
                rows[row][num] = cols[col][num] = boxs[box][num] = false;
            }
        }
        return false;
    }
};
```

