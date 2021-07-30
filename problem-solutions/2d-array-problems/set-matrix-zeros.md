# Set Matrix Zeros

[InterviewBit](https://www.interviewbit.com/problems/set-matrix-zeros/)

[Leetcode 73](https://app.gitbook.com/@thangarajn1992/s/leetcode/v/main/difficulty-based-problem-index/leetcode-medium/leetcode-73-set-matrix-zeroes)

### Problem Statement

Given a matrix, **A** of size **M** x **N** of **0s** and **1s**. If an element is **0**, set its entire row and column to **0**.

**Note**: This will be evaluated on the extra memory used. Try to minimize the space and time complexity.

**Constraints:**

```text
1 <= N, M <= 1000
0 <= A[i][j] <= 1
```

**Examples:**

```text
Input 1:
    [   [1, 0, 1],
        [1, 1, 1], 
        [1, 1, 1]   ]

Output 1:
    [   [0, 0, 0],
        [1, 0, 1],
        [1, 0, 1]   ]

Input 2:
    [   [1, 0, 1],
        [1, 1, 1],
        [1, 0, 1]   ]

Output 2:
    [   [0, 0, 0],
        [1, 0, 1],
        [0, 0, 0]   ]
```

### Solution

```cpp
void Solution::setZeroes(vector<vector<int> > &A) {
    set<int> reset_rows;
    set<int> reset_cols;

    for(int row = 0; row < A.size(); row++)
    {
        for(int col = 0; col < A[0].size(); col++)
        {
            if(A[row][col] == 0)
            {
                reset_rows.insert(row);
                reset_cols.insert(col);
            }
        }
    }

    for(int row = 0; row < A.size(); row++)
    {
        for(int col = 0; col < A[0].size(); col++)
        {  
            if(reset_rows.count(row) || reset_cols.count(col))
                A[row][col] = 0;
        }
    } 
}
```

