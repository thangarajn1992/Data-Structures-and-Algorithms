# Generate Matrix in Spiral Order

[Leetcode 59](https://leetcode.com/problems/spiral-matrix-ii/)

[InterviewBit](https://www.interviewbit.com/problems/spiral-order-matrix-ii/)

### Problem Statement

Given a positive integer `n`, generate an `n x n` `matrix` filled with elements from `1` to `n2` in spiral order.

**Example 1:** ![](https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg)

```text
Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]
```

**Example 2:**

```text
Input: n = 1
Output: [[1]]
```

**Constraints:**

* `1 <= n <= 20`

### Implementation

```cpp
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> result(n, vector<int>(n,0));
        vector<vector<int>> dir = {{0,1}, {1, 0}, {0,-1}, {-1,0}};
        int total_elements = n * n;
        int count = 1;
        int cur_r = 0, cur_c = 0, cur_dir = 0;
        vector<vector<bool>> visited(n, vector<bool>(n,false));
        while(count <= total_elements)
        {
            result[cur_r][cur_c] = count;
            count++;
            visited[cur_r][cur_c] = true;
            int next_r = cur_r + dir[cur_dir][0];
            int next_c = cur_c + dir[cur_dir][1];
            if(next_r < 0 || next_r >= n ||
               next_c < 0 || next_c >= n ||
               visited[next_r][next_c] == true) // change the direction
            {
                cur_dir = (cur_dir + 1) % 4;
                next_r = cur_r + dir[cur_dir][0];
                next_c = cur_c + dir[cur_dir][1];
            }
            cur_r = next_r;
            cur_c = next_c; 
        }
        return result;        
    }
};
```

