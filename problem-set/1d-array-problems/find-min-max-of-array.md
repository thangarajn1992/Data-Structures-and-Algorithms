# Find Min Max of Array

[InterviewBit](https://www.interviewbit.com/problems/max-min-05542f2f-69aa-4253-9cc7-84eb7bf739c4/)



### Problem Statement

Given an array A of size N. You need to find the sum of **Maximum and Minimum element** in the given array. **NOTE:** You should make minimum number of comparisons.

**Problem Constraints**

* 1 &lt;= N &lt;= 10^5
* -10^9 &lt;= A\[i\] &lt;\] 10^9

```text
 Input 1:
 A = [-2, 1, -4, 5, 3]
 Output 1:
 1  ( -4 + 5 )
 
 Input 2:
 A = [1, 3, 4, 1]
 Output:
 5
```

### Solution

```cpp
pair<int,int> find_min_max(vector<int>&A, int start, int end)
{
    if(start == end)
        return make_pair(A[start], A[start]);
    if(end - start == 1)
        return make_pair(min(A[start], A[end]), max(A[start], A[end]));
    
    int mid = start + (end - start)/2;
    pair<int,int> first_half = find_min_max(A, start, mid);
    pair<int,int> second_half = find_min_max(A, mid+1, end);
    return make_pair(min(first_half.first, second_half.first), 
                     max(first_half.second, second_half.second));    
}

int Solution::solve(vector<int> &A) {
    pair<int,int> result = find_min_max(A, 0, A.size()-1);
    return result.first + result.second;
}
```

