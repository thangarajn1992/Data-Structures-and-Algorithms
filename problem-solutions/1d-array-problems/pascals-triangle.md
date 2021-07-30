# Pascal's Triangle & Kth row of Pascal Triangle

[Leetcode 118](https://leetcode.com/problems/pascals-triangle/)       [Leetcode 119](https://leetcode.com/problems/pascals-triangle-ii/)

[Interviewbit-PascalTriangle  ](https://www.interviewbit.com/problems/pascal-triangle/)      [InterviewBit-kth Row of Pascal](https://www.interviewbit.com/problems/kth-row-of-pascals-triangle/)

### Problem Statement

In **Pascal's triangle**, each number is the sum of the two numbers directly above it as shown: ![](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

**Example 1:**

```text
Input: numRows = 5
Output: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
```

**Example 2:**

```text
Input: numRows = 1
Output: [[1]]
```

### Solution

```cpp
vector<vector<int> > Solution::solve(int A) {
    if(A == 0)
        return {};
    vector<vector<int>> pascal_triangle(A);
    pascal_triangle[0] = {1};
    for(int i = 1; i < A; i++)
    {
        pascal_triangle[i].push_back(pascal_triangle[i-1][0]);
        for(int j = 1; j < i; j++)  // (i-1)th row will have i elements in pascal triangle
            pascal_triangle[i].push_back(pascal_triangle[i-1][j-1] + pascal_triangle[i-1][j]);
        pascal_triangle[i].push_back(pascal_triangle[i-1].back());
    }
    return pascal_triangle;
}
```

## Generate kth Row of Pascal Triangle

[Leetcode 119](https://leetcode.com/problems/pascals-triangle-ii/)     [InterviewBit-kth Row of Pascal](https://www.interviewbit.com/problems/kth-row-of-pascals-triangle/)

### Problem Statement

Given an integer `rowIndex`, return the `rowIndexth` \(**0-indexed**\) row of the **Pascal's triangle**.

In **Pascal's triangle**, each number is the sum of the two numbers directly above it as shown: ![](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

**Example 1:**

```text
Input: rowIndex = 3
Output: [1,3,3,1]
```

**Example 2:**

```text
Input: rowIndex = 0
Output: [1]
```

**Example 3:**

```text
Input: rowIndex = 1
Output: [1,1]
```

**Constraints:**

* `0 <= rowIndex <= 33`

### Solution

```cpp
class Solution {
public:
    vector<int> getRow(int rowIndex) {
        vector<vector<int>> result(rowIndex+1);
        result[0] = {1};
        for(int i = 1; i <= rowIndex; i++)
        {
            result[i].push_back(result[i-1][0]);
            for(int j = 1; j < i; j++) // i-1 will have "i" elements in pascal
                result[i].push_back(result[i-1][j-1] + result[i-1][j]);
            result[i].push_back(result[i-1][i-1]);
        }
        return result.back();
    }
};
```

