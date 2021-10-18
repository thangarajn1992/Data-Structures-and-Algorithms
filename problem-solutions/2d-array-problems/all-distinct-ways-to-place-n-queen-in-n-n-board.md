# All Distinct ways to place N Queen in N\*N Board

### Source

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/n-queen-problem0315/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

The n-queens puzzle is the problem of placing **n** queens on a (**n×n)** chessboard such that no two queens can attack each other. Given an integer n, find all distinct solutions to the n-queens puzzle. Each solution contains distinct board configurations of the n-queens’ placement, where the solutions are a permutation of \[1,2,3..n] in increasing order, here the number in the _ith_ place denotes that the _ith_-column queen is placed in the row with that number. For eg below figure represents a chessboard \[3 1 4 2].\
\
 ![](https://contribute.geeksforgeeks.org/wp-content/uploads/ratinmaze_filled11-1.png)

**Example 1:**

```
Input:
1
Output:
[1]
Explaination:
Only one queen can be placed 
in the single cell available.
```

**Example 2:**

```
Input:
4
Output:
[2 4 1 3 ] [3 1 4 2 ]
Explaination:
These are the 2 possible solutions.
```

**Expected Time Complexity:** O(n!)\
**Expected Auxiliary Space:** O(n^2) 

**Constraints:**\
 1 ≤ n ≤ 10 

### Solution

```cpp
class Solution{
public:
    int size;
    vector<vector<int>> combinations;
    vector<int> board_state;
    vector<bool> cols;
    vector<bool> diagonals;
    vector<bool> antidiagonals;

    void backtrack(int row)
    {
        if(row >= size) // end-case
        {
            combinations.push_back(board_state);
            return;
        }
        
        for(int col = 0; col < size; col++)
        {
            int currDiagonal = (row - col) + size - 1;
            int currAntiDiagonal = row + col;
            
            // Can we place queen here ?
            if( !cols[col] && !diagonals[currDiagonal] &&
                !antidiagonals[currAntiDiagonal])
            {            
                // "Add" the queen to the board
                cols[col] = true;
                diagonals[currDiagonal] = true;
                antidiagonals[currAntiDiagonal] = true;
                board_state[row] = col+1;
            
                // Move to next row with updated board state
                backtrack(row+1);
            
                // Remove this queen from board and check for other possiblities
                cols[col] = false;
                diagonals[currDiagonal] = false;
                antidiagonals[currAntiDiagonal] = false;
                board_state[row] = 0;
            }
        }
    }
    
    vector<vector<int>> nQueen(int n) {
        size = n;
        board_state.resize(n, 0);
        cols.resize(n,false);
        diagonals.resize(2*n - 1, false); 
        antidiagonals.resize(2*n - 1, false);
        backtrack(0);
        return combinations;
    }
};
```
