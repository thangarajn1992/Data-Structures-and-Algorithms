# Make neighbors of Zero as Zero and the neighbor's sum into element that had zero

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/make-zeroes4042/1#)

### Companies

### Problem Statement

Given a matrix of  size n x m. Your task is to make Zeroes, that means in whole matrix when you find a zero, convert its upper, lower, left, and right value to zero and make that element the sum of the upper, lower, left and right value. Do the following tasks according to the initial matrix. Your task is to complete the function **MakeZeros()** which takes the matrix as input parameter and does the given task according to initial matrix. You don't need to return anything. The driver code prints the modified matrix itself in the output.\
&#x20;&#x20;

**Example 1:**

```
Input: matrix = {{1, 2, 3, 4},
                 {5, 6, 0, 7}, 
                 {8, 9, 4, 6},
                 {8, 4, 5, 2}}
Output: {{1, 2, 0, 4}, 
         {5, 0, 20, 0},
         {8, 9, 0, 6}, 
         {8, 4, 5, 2}}
Explanation: As matrix[1][2] = 0, we will
perform the operation here. Then matrix[1][2]
= matrix[0][2] + matrix[2][2] + matrix[1][1] 
+ matrix[1][3] and matrix[0][2] = matrix[2][2] 
= matrix[1][1] = matrix[1][3] = 0.
```

**Example 2:**

```
Input: matrix = {{1, 2}, 
                 {3, 4}}
output: {{1, 2}, 
         {3, 4}}
```

**Expected Time Complexity:** O(n \* m)\
**Expected Space Complexity:** O(n \* m)\
&#x20;&#x20;

**Constraints:**\
&#x20;`1 ≤ n, m ≤ 100`\
&#x20;`1 ≤ matrix[i][j] ≤ 100`, where `0 ≤ i ≤ n` and `0 ≤ j ≤ m`

### Solution

```cpp
class Solution {
public:
    void MakeZeros(vector<vector<int> >& matrix) {
        vector<vector<int>> zeroEntries;
        int rows = matrix.size();
        int cols = matrix[0].size();
        for(int row = 0; row < rows; row++)
        {
            for(int col = 0; col < cols; col++)
            {
                if(matrix[row][col] == 0)
                    zeroEntries.push_back({row,col});
            }
        }
        
        vector<vector<int>> temp(matrix);
        vector<vector<int>> dir = {{0,1}, {0,-1}, {1,0}, {-1,0}};
        for(int index = 0; index < zeroEntries.size(); index++)
        {
            int neighbor_sum = 0;
            for(int d = 0; d < 4; d++)
            {
                int nr = zeroEntries[index][0] + dir[d][0];
                int nc = zeroEntries[index][1] + dir[d][1];
                
                if(nr >= 0 && nr < rows && nc >= 0 && nc < cols)
                {
                    neighbor_sum += temp[nr][nc];
                    matrix[nr][nc] = 0;
                }
            }
            matrix[zeroEntries[index][0]][zeroEntries[index][1]] = neighbor_sum;
        }
    }
};
```
