# Maximum path sum in matrix with Down, Diagonal Down, Anti-Diagonal Down directions

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/path-in-matrix3805/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Flipkart](../../company-based-lists/flipkart.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Samsung](../../company-based-lists/samsung.md)

### Problem Statement

Given a NxN matrix of positive integers. There are only three possible moves from a cell **Matrix\[r\]\[c\]**.

1. Matrix \[r+1\] \[c\]
2. Matrix \[r+1\] \[c-1\]
3. Matrix \[r+1\] \[c+1\]

Starting from any column in row 0 return the largest sum of any of the paths up to row N-1.  
  
 **Example 1:**

```text
Input: N = 2
Matrix = {{348, 391},
          {618, 193}}
Output: 1009
Explaination: The best path is 391 -> 618. 
It gives the sum = 1009.
```

  
 **Example 2:**

```text
Input: N = 2
Matrix = {{2, 2},
          {2, 2}}
Output: 4
Explaination: No matter which path is 
chosen, the output is 4.
```

  
 **Your Task:**  
 You do not need to read input or print anything. Your task is to complete the function **maximumPath\(\)** which takes the size N and the Matrix as input parameters and returns the highest maximum path sum.

  
 **Expected Time Complexity:** O\(N\*N\)  
 **Expected Auxiliary Space:** O\(N\*N\)

  
 **Constraints:**  
 1 ≤ N ≤ 500  
 1 ≤ Matrix\[i\]\[j\] ≤ 1000

### Solution

#### DFS + Dynamic Programming

```cpp
class Solution{
public:
    vector<vector<int>> preCalc;
    int maximumPath(int N, vector<vector<int>> Matrix)
    {
        preCalc.resize(N, vector<int>(N, -1));
        for(int col = 0; col < N; col++)
            preCalc[N-1][col] = Matrix[N-1][col];
        
        int maxCost = INT_MIN;
        for(int col = 0; col < N; col++)
             maxCost = max(maxCost, maximumPathUtil(Matrix, 0, col, N));
        
        return maxCost;
    }
    int maximumPathUtil(vector<vector<int>>&Matrix, int row, int col, int size)
    {
        
        if(row < 0 || row >= size || col < 0 || col >= size)
            return 0;
        
        if(preCalc[row][col] != -1)
            return preCalc[row][col];
        
        int maxCost = maximumPathUtil(Matrix, row+1, col, size);
        maxCost = max(maxCost, maximumPathUtil(Matrix, row+1, col-1, size));
        maxCost = max(maxCost, maximumPathUtil(Matrix, row+1, col+1, size));
        
        preCalc[row][col] = Matrix[row][col] + maxCost;
        return preCalc[row][col];
    }
};
```



