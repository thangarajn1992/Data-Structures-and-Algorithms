# Find Winner on a Tic Tac Toe Game from given moves

### Sources

* [Leetcode 1275](https://leetcode.com/problems/find-winner-on-a-tic-tac-toe-game/)

### Companies

### Problem Statement

Tic-tac-toe is played by two players _A_ and _B_ on a 3 x 3 grid.

Here are the rules of Tic-Tac-Toe:

* Players take turns placing characters into empty squares \(" "\).
* The first player _A_ always places "X" characters, while the second player _B_ always places "O" characters.
* "X" and "O" characters are always placed into empty squares, never on filled ones.
* The game ends when there are 3 of the same \(non-empty\) character filling any row, column, or diagonal.
* The game also ends if all squares are non-empty.
* No more moves can be played if the game is over.

Given an array `moves` where each element is another array of size 2 corresponding to the row and column of the grid where they mark their respective character in the order in which _A_ and _B_ play.

Return the winner of the game if it exists \(_A_ or _B_\), in case the game ends in a draw return "Draw", if there are still movements to play return "Pending".

You can assume that `moves` is **valid** \(It follows the rules of Tic-Tac-Toe\), the grid is initially empty and _A_ will play **first**.

**Example 1:**

```text
Input: moves = [[0,0],[2,0],[1,1],[2,1],[2,2]]
Output: "A"
Explanation: "A" wins, he always plays first.
"X  "    "X  "    "X  "    "X  "    "X  "
"   " -> "   " -> " X " -> " X " -> " X "
"   "    "O  "    "O  "    "OO "    "OOX"
```

**Example 2:**

```text
Input: moves = [[0,0],[1,1],[0,1],[0,2],[1,0],[2,0]]
Output: "B"
Explanation: "B" wins.
"X  "    "X  "    "XX "    "XXO"    "XXO"    "XXO"
"   " -> " O " -> " O " -> " O " -> "XO " -> "XO " 
"   "    "   "    "   "    "   "    "   "    "O  "
```

**Example 3:**

```text
Input: moves = [[0,0],[1,1],[2,0],[1,0],[1,2],[2,1],[0,1],[0,2],[2,2]]
Output: "Draw"
Explanation: The game ends in a draw since there are no moves to make.
"XXO"
"OOX"
"XOX"
```

**Example 4:**

```text
Input: moves = [[0,0],[1,1]]
Output: "Pending"
Explanation: The game has not finished yet.
"X  "
" O "
"   "
```

**Constraints:**

* `1 <= moves.length <= 9`
* `moves[i].length == 2`
* `0 <= moves[i][j] <= 2`
* There are no repeated elements on `moves`.
* `moves` follow the rules of tic tac toe.

### Solution

```cpp
class Solution {
private:
    // Initialize the board, n = 3 in this problem.
    int n = 3;
    vector<vector<int>> board;

public:
    string tictactoe(vector<vector<int>>& moves) {        
        board.assign(n, vector<int>(n, 0));
        int player = 1;

        // For each move
        for (vector<int> move : moves) 
        {
            int row = move[0];
            int col = move[1];

            // Mark the current move with the current playrer's id.
            board[row][col] = player;

            // If any of the winning conditions is met, return the current player's id.
            if (checkRow(row, player) || 
                checkCol(col, player) || 
                (row == col && checkDiagonal(player)) ||
                (row + col == n - 1 && checkAntiDiagonal(player))) 
            {
                return player == 1 ? "A" : "B";
            }

            // If no one wins so far, change to the other player alternatively. 
            // That is from 1 to -1 or from -1 to 1.
            player *= -1;
        }

        // If all moves are completed and there is still no result, we shall check if 
        // the grid is full or not. If so, the game ends with draw, otherwise pending.
        return moves.size() == 3 * 3 ? "Draw" : "Pending";
    }
    
    // Check if any of 4 winning conditions to see if the current player has won.
    bool checkRow(int row, int player) {
        for (int col = 0; col < n; ++col) 
            if (board[row][col] != player) 
                return false;
        
        return true;
    }
    
    bool checkCol(int col, int player) {
        for (int row = 0; row < n; ++row) 
            if (board[row][col] != player) 
                return false;
        
        return true;
    }
        
    bool checkDiagonal(int player) {
        for (int row = 0; row < n; ++row) 
            if (board[row][row] != player) 
                return false;

        return true;
    }
        
    bool checkAntiDiagonal(int player) {
        for (int row = 0; row < n; ++row) 
            if (board[row][n - 1 - row] != player) 
                return false;

        return true;
    }
};  
```

