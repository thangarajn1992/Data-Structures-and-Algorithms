# Pick N items with Maximum sum from both ends

[Interview-Bit](https://www.interviewbit.com/problems/pick-from-both-sides/)

### Problem Statement

Given an integer array **A** of size **N**. You can pick **B** elements from either left or right end of the array **A** to get maximum sum. Find and return this **maximum possible sum**.

Suppose B = 4 and array A contains 10 elements then You can pick first four elements or can pick last four elements or can pick 1 from front and 3 from back etc . you need to return the maximum possible sum of elements you can pick.  
  
**Problem Constraints**

1 &lt;= N &lt;= 10^5

1 &lt;= B &lt;= N

-10^3 &lt;= A\[i\] &lt;= 10^3

**Input Format**  
First argument is an integer array **A**.  Second argument is an integer **B**.

**Output Format**  
Return an integer denoting the maximum possible sum of elements you picked.  


**Example**

```text
 Input 1:
 A = [5, -2, 3 , 1, 2]
 B = 3
 Output 1:
 8
 
 Input 2:
 A = [1, 2]
 B = 1
 Output 2:
```

### Solution

```cpp
int Solution::solve(vector<int> &A, int B) {
    int size = A.size();
    vector<long long int> prefix_sum(size + 1, 0);
    for(int i = 1; i <= size; i++)
        prefix_sum[i] = prefix_sum[i-1] + A[i-1];
    
    int max_sum = INT_MIN;
    for(int i = 0; i <= B; i++)
    {
        int front_sum = prefix_sum[B-i];
        int back_sum = prefix_sum[size] - prefix_sum[size - i];
        max_sum = max(max_sum, front_sum + back_sum);
    }
    return max_sum;
}
```

