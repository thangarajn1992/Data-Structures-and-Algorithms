# Spiral Traversal from Any Co-ordinate

[Leetcode 885](https://leetcode.com/problems/spiral-matrix-iii/)

### Problem Statement

On a 2 dimensional grid with `rows` rows and `cols` columns, we start at `(rStart, cStart)` facing east.

Here, the north-west corner of the grid is at the first row and column, and the south-east corner of the grid is at the last row and column.

Now, we walk in a clockwise spiral shape to visit every position in this grid. 

Whenever we would move outside the boundary of the grid, we continue our walk outside the grid \(but may return to the grid boundary later.\) 

Eventually, we reach all `rows * cols` spaces of the grid.

Return a list of coordinates representing the positions of the grid in the order they were visited.

**Example 1:**

```text
Input: rows = 1, cols = 4, rStart = 0, cStart = 0
Output: [[0,0],[0,1],[0,2],[0,3]]
```

**Example 2:**

```text
Input: rows = 5, cols = 6, rStart = 1, cStart = 4
Output: [[1,4],[1,5],[2,5],[2,4],[2,3],[1,3],[0,3],[0,4],[0,5],[3,5],[3,4],[3,3],[3,2],
         [2,2],[1,2],[0,2],[4,5],[4,4],[4,3],[4,2],[4,1],[3,1],[2,1],[1,1],[0,1],[4,0],
         [3,0],[2,0],[1,0],[0,0]]
```

**Note:**

1. `1 <= rows <= 100`
2. `1 <= cols <= 100`
3. `0 <= rStart < rows`
4. `0 <= cStart < cols`

### Approach

We can walk in a spiral shape from the starting square, ignoring whether we stay in the grid or not. Eventually, we must have reached every square in the grid.

**Algorithm**

Examining the lengths of our walk in each direction, we find the following pattern: `1, 1, 2, 2, 3, 3, 4, 4, ...` That is, we walk 1 unit east, then 1 unit south, then 2 units west, then 2 units north, then 3 units east, etc. Because our walk is self-similar, this pattern repeats in the way we expect.

After, the algorithm is straightforward: perform the walk and record positions of the grid in the order we visit them. Please read the inline comments for more details.

```cpp
class Solution {
public:
    vector<vector<int>> spiralMatrixIII(int rows, int cols, int rStart, int cStart) {
        vector<vector<int>> dir = { {0,1}, {1,0}, {0,-1}, {-1,0}};
        int total_elements = rows*cols;
        vector<vector<int>> result(total_elements);
        int count = 0;
        result[count++] = {rStart, cStart} ;
        
        if(total_elements == 1)
            return result;
        
        // After each spiral, the start step increases by 2
        // Eg: 1 ->east 1->south 2->west 2->north
        // 2nd Spiral 3->east 3->south 4->west 4->north
        cur_spiral_start_step = 1;
        while(count < total_elements)
        {
            // For each spiral move through all 4 directions
            for(int cur_dir = 0; cur_dir < 4; cur_dir++)
            {
                int cur_steps = cur_spiral_start_step + (cur_dir/2);
                for(int move = 0; move < cur_steps; move++)
                {
                    rStart = rStart + dir[cur_dir][0];
                    cStart = cStart + dir[cur_dir][1];
                    // If valid entry, add the co-ordinate into result
                    if(rStart >= 0 && rStart < rows &&
                       cStart >= 0 && cStart < cols)
                    {
                        result[count++] = {rStart, cStart};
                        if(count == total_elements)
                            return result;
                    }
                }
            }
            // For next spiral, incr it by 2
            cur_spiral_start_step += 2;            
        }
        return vector<vector<int>>{};
    }
};
```

