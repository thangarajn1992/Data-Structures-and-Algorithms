# Minimum Cost Path with 4 possible directions

### Source

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/minimum-cost-path3833/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Samsung](../../company-based-lists/samsung.md)
* [Goldman Sachs](../../company-based-lists/goldman-sachs.md)

### Problem Statement

Given a square **grid** of size **N**, each cell of which contains integer cost which represents a cost to traverse through that cell, we need to find a path from top left cell to bottom right cell by which the total cost incurred is minimum.\
 From the cell (i,j) we can go (i,j-1), (i, j+1), (i-1, j), (i+1, j). 

**Note: **It is assumed that negative cost cycles do not exist in the input matrix.

**Example 1:**

```
Input: grid = {{9,4,9,9},{6,7,6,4},
{8,3,3,7},{7,4,9,10}}
Output: 43
Explanation: 
The grid is-
9 4 9 9
6 7 6 4
8 3 3 7
7 4 9 10
The minimum cost is
9 + 4 + 7 + 3 + 3 + 7 + 10 = 43.
```

**Example 2:**

```
Input: grid = {{4,4},{3,7}}
Output: 14
Explanation: 
The grid is-
4 4
3 7
The minimum cost is 4 + 3 + 7 = 14.
```

**Expected Time Compelxity: **O(n^2\*log(n))\
**Expected Auxiliary Space:** O(n^2) 

**Constraints:**\
 1 ≤ n ≤ 500\
 1 ≤ cost of cells ≤ 1000

### Solution

### Dijkstra's Algorithm 

```cpp
// structure for information of each cell
struct cell
{
    int x, y;
    int distance;
    cell(int x, int y, int distance) :
        x(x), y(y), distance(distance) {}
};

// Utility method for comparing two cells
bool operator<(const cell& a, const cell& b)
{
    if (a.distance == b.distance)
    {
        if (a.x == b.x)
            return (a.y < b.y);
        else
            return (a.x < b.x);
    }
    return (a.distance < b.distance);
}

class Solution
{
public:
    int minimumCostPath(vector<vector<int>>& grid) 
    {
        int rows = grid.size(), cols = grid[0].size();
        vector<vector<int>> cost(rows, vector<int>(cols, INT_MAX));
        vector<vector<int>> dir = {{1,0}, {0,1}, {-1,0}, {0,-1}};

        set<cell> st;
        st.insert(cell(0, 0, 0));

        cost[0][0] = grid[0][0];

        // loop for standard dijkstra's algorithm
        while (!st.empty())
        {
            cell k = *st.begin();  // cell with next minimum cost
            st.erase(st.begin());

            // looping through all neighbours
            for (int d = 0; d < 4; d++)
            {
                int x = k.x + dir[d][0];
                int y = k.y + dir[d][1];

                // if inside boundary and
                // If distance from current cell is smaller, then
                // update distance of neighbour cell
                if(x >= 0 && x < rows && y >= 0 && y < cols &&
                cost[x][y] > cost[k.x][k.y] + grid[x][y])
                {
                    // If cell is already there in set, then
                    // remove its previous entry
                    if (cost[x][y] != INT_MAX)
                        st.erase(st.find(cell(x, y, cost[x][y])));

                    // update the distance and insert new updated
                    // cell in set
                    cost[x][y] = cost[k.x][k.y] + grid[x][y];
                    st.insert(cell(x, y, cost[x][y]));
                }
            }
        }
        return cost[rows - 1][cols - 1];
    }      
};
```
