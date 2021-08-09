# Check if Move is Legal

### Sources

* [Leetcode 1958](https://leetcode.com/problems/check-if-move-is-legal/)

### Problem Statement

You are given a **0-indexed** `8 x 8` grid `board`, where `board[r][c]` represents the cell `(r, c)` on a game board. On the board, free cells are represented by `'.'`, white cells are represented by `'W'`, and black cells are represented by `'B'`.

Each move in this game consists of choosing a free cell and changing it to the color you are playing as \(either white or black\). However, a move is only **legal** if, after changing it, the cell becomes the **endpoint of a good line** \(horizontal, vertical, or diagonal\).

A **good line** is a line of **three or more cells \(including the endpoints\)** where the endpoints of the line are **one color**, and the remaining cells in the middle are the **opposite color** \(no cells in the line are free\). You can find examples for good lines in the figure below: 

![](https://assets.leetcode.com/uploads/2021/07/22/goodlines5.png)

Given two integers `rMove` and `cMove` and a character `color` representing the color you are playing as \(white or black\), return `true` _if changing cell_ `(rMove, cMove)` _to color_ `color` _is a **legal** move, or_ `false` _if it is not legal_.

**Example 1:** ![](https://assets.leetcode.com/uploads/2021/07/10/grid11.png)

```text
Input: board = [[".",".",".","B",".",".",".","."],[".",".",".","W",".",".",".","."],[".",".",".","W",".",".",".","."],[".",".",".","W",".",".",".","."],["W","B","B",".","W","W","W","B"],[".",".",".","B",".",".",".","."],[".",".",".","B",".",".",".","."],[".",".",".","W",".",".",".","."]], rMove = 4, cMove = 3, color = "B"
Output: true
Explanation: '.', 'W', and 'B' are represented by the colors blue, white, and black respectively, and cell (rMove, cMove) is marked with an 'X'.
The two good lines with the chosen cell as an endpoint are annotated above with the red rectangles.
```

**Example 2:** ![](https://assets.leetcode.com/uploads/2021/07/10/grid2.png)

```text
Input: board = [[".",".",".",".",".",".",".","."],[".","B",".",".","W",".",".","."],[".",".","W",".",".",".",".","."],[".",".",".","W","B",".",".","."],[".",".",".",".",".",".",".","."],[".",".",".",".","B","W",".","."],[".",".",".",".",".",".","W","."],[".",".",".",".",".",".",".","B"]], rMove = 4, cMove = 4, color = "W"
Output: false
Explanation: While there are good lines with the chosen cell as a middle cell, there are no good lines with the chosen cell as an endpoint.
```

**Constraints:**

* `board.length == board[r].length == 8`
* `0 <= rMove, cMove < 8`
* `board[rMove][cMove] == '.'`
* `color` is either `'B'` or `'W'`.

### Solution 

```cpp
class Solution {
public:
    bool checkMove(vector<vector<char>>& board, int rMove, int cMove, char color) {
        board[rMove][cMove] = color;
        vector<vector<int>> dir = {{0, 1}, // East
                                   {0, -1}, // West
                                   {-1, 0}, // North
                                   {1, 0}, // South
                                   {1, 1}, // South-East
                                   {-1,-1}, // North-West
                                   {-1, 1}, // North-East
                                   {1, -1}}; // South-West
        int length;
        int board_size = 8;
        int cur_row = rMove, cur_col = cMove;
        char opp_color = ( color == 'B') ? 'W' : 'B';
        for(int d = 0; d < 8; d++)
        {
            length = 1;
            cur_row = rMove + dir[d][0];
            cur_col = cMove + dir[d][1];
            
            while(cur_row >= 0 && cur_row < board_size &&
                  cur_col >= 0 && cur_col < board_size)
            {
                if(length == 1)
                {
                    if(board[cur_row][cur_col] == opp_color)
                        length++;
                    else
                        break;
                }
                else
                {
                    if(board[cur_row][cur_col] == color)
                        return true;
                    else if(board[cur_row][cur_col] == '.')
                        break;
                    else
                        length++;
                }
                cur_row += dir[d][0];
                cur_col += dir[d][1];
            }  
        }
        return false;
    }
};
```

