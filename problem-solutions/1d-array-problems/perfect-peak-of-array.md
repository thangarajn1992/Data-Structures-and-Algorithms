# Element greater than left elements & lesser than right elements

[InterviewBit](https://www.interviewbit.com/problems/perfect-peak-of-array/)

### Problem Statement

Given an integer array **A** of size **N**.

You need to check that whether there exist a element which is **strictly greater than all the elements on left** of it and **strictly smaller than all the elements** on right of it. If it exists return **1** else return **0**. Do not consider the corner elements i.e **A\[0] and A\[N-1]** as the answer.\


**Constraints**

* 3 <= N <= 10^5
* 1 <= A\[i] <= 10^9

```
Example 1:
Input    :    A = [5, 1, 4, 3, 6, 8, 10, 7, 9]
Output   :    1
Explanation:   
A[4] = 6 is the element we are looking for.
All elements on left of A[4] are smaller than it and all elements on right are greater.

Example 2:
Input    :    A = [5, 1, 4, 4]
Output   :    0    
```

### Solution

#### Easier to understand solution

```cpp
int Solution::perfectPeak(vector<int> &A) {
    int size = A.size();
    int left_max[size];
    left_max[0] = A[0];
    for(int i = 1; i < size; i++)
        left_max[i] = max(left_max[i-1], A[i]);

    int right_min[size];
    right_min[size-1] = A[size-1];
    for(int i = size - 2; i >= 0; i--)
        right_min[i] = min(right_min[i+1], A[i]);

    for(int i = size - 2; i > 0; i--)
        if(A[i] > left_max[i-1] && A[i] < right_min[i+1])
            return true;

    return false;
}
```

#### My Solution

```cpp
int Solution::perfectPeak(vector<int> &A) {
    bool peak_found = false;
    int size = A.size();
    int max_so_far = A[0];
    int peak = A[0];
    for(int i = 1; i < size; i++)
    {
        if(peak >= A[i])
        {
            peak_found = false;
            peak = max_so_far;
        }
        else if(peak < A[i])
        {
            max_so_far = max(max_so_far, A[i]);
            if(peak_found == false && i != size - 1)
            {
                peak_found = true;
                peak = max_so_far;
            }
        }
    }
    return peak_found;
}
```
