# Number of Palindromic paths in a Matrix

### Source

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/number-of-palindromic-paths-in-a-matrix0819/1#)

### Companies

* [Samsung](../../company-based-lists/samsung.md)

### Problem Statement

Given a **matrix** containing lower alphabetical characters only of size **n\*m**. We need to count the number of palindromic paths in the given matrix.\
 A path is defined as a sequence of cells starting from top-left cell and ending at bottom-right cell. We are allowed to move to **right** and **down** only from current cell.

**Example 1:**

```
Input: matrix = {{a,a,a,b},{b,a,a,a},{a,b,b,a}}
Output: 3
Explanation: Number of palindromic paths are 3 
from top-left to bottom-right.
aaaaaa (0, 0) -> (0, 1) -> (1, 1) -> (1, 2) -> 
(1, 3) -> (2, 3)    
aaaaaa (0, 0) -> (0, 1) -> (0, 2) -> (1, 2) -> 
(1, 3) -> (2, 3)    
abaaba (0, 0) -> (1, 0) -> (1, 1) -> (1, 2) -> 
(2, 2) -> (2, 3)
```

**Example 2:**

```
Input: matrix = {{a,b},{c,d}}
Output: 0
Explanation: There is no palindromic paths.
```

**Expected Time Complexity: **O(n^2\*m^2)\
**Space Complexity: **O(n\*m)\
**Constraints: **1 ≤ n, m ≤ 100

### Solution

```cpp
class Solution {
  public:
    // vector<int> will have (Sx, Sy, Ex, Ey) i.e. 
    //(Sx,Sy) is current cell in traversing path from top left
    //(Ex,Ey) is current cell in traversing path from Bottom right
    map<vector<int>, int> seen;
    int mod = pow(10,9) + 7;
    int countPalindromicPaths(vector<vector<char>>matrix){
        return findPaths(matrix, 0, 0, matrix.size()-1, matrix[0].size()-1);
    }
    
    int findPaths(vector<vector<char>>&matrix, int Sx, int Sy, int Ex, int Ey)
    {
        // Base case 1: Two paths crossed each other zone
        if(Sx > Ex || Sy > Ey)
           return 0;
        
        // Base case 2: Not palindrome  
        if(matrix[Sx][Sy] != matrix[Ex][Ey])
            //not a palindrome
            return 0;
        
        // Base case 3: Adjacent cells and equal
        if(abs((Sx - Ex) + (Sy - Ey)) <= 1)
            return 1;
         
        // Pre-calculated   
        if(seen.find({Sx, Sy, Ex, Ey}) != seen.end())
            return seen[{Sx, Sy, Ex, Ey}];
        
        // check for other possibilities
        // Path from Top Left cell, can go DOWN(Sx+1) or RIGHT(Sy+1)
        // Path from Bottom Right cell, can go UP(Ex-1) or LEFT(Ey-1)
        long long int possibilities = 0;
        possibilities += findPaths(matrix, Sx+1, Sy, Ex-1, Ey);
        possibilities += findPaths(matrix, Sx+1, Sy, Ex, Ey-1);
        possibilities += findPaths(matrix, Sx, Sy+1, Ex-1, Ey);
        possibilities += findPaths(matrix, Sx, Sy+1, Ex, Ey-1);
        
        possibilities %= mod;
        
        seen[{Sx, Sy, Ex, Ey}] = possibilities;
        return possibilities;
    }
};
```
