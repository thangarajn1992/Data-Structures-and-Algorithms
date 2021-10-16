# Count distinct elements in every window

### Sources

* [GeeksForGeeks](https://practice.geeksforgeeks.org/problems/count-distinct-elements-in-every-window/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given an array of integers and a number K. Find the count of distinct elements in every window of size K in the array.

**Example 1:**

```
Input:
N = 7, K = 4
A[] = {1,2,1,3,4,2,3}
Output: 3 4 4 3
Explanation: Window 1 of size k = 4 is
1 2 1 3. Number of distinct elements in
this window are 3. 
Window 2 of size k = 4 is 2 1 3 4. Number
of distinct elements in this window are 4.
Window 3 of size k = 4 is 1 3 4 2. Number
of distinct elements in this window are 4.
Window 4 of size k = 4 is 3 4 2 3. Number
of distinct elements in this window are 3.
```

**Example 2:**

```
Input:
N = 3, K = 2
A[] = {4,1,1}
Output: 2 1
```

**Your Task:**\
Your task is to complete the function **countDistinct()** which takes the array A\[], the size of the array(N), and the window size(K) as inputs and returns an array containing the count of distinct elements in every contiguous window of size K in the array A\[].

**Expected Time Complexity:** O(N).\
**Expected Auxiliary Space:** O(N).

**Constraints:**\
1 <= K <= N <= 10^5\
1 <= A\[i] <= 10^5 , for each valid i

### Solution

```cpp
class Solution{
  public:
    vector <int> countDistinct (int A[], int n, int k)
    {
        vector<int> distinctIntegersPerWindow;
        map<int,int> integers;
        int distinctCnt = 0;
        for(int index = 0; index < k; index++)
        {
            if(integers[A[index]] == 0)
                distinctCnt++;
            integers[A[index]]++;
        }
        distinctIntegersPerWindow.push_back(distinctCnt);
        
        for(int index = k; index < n; index++)
        {
            if(integers[A[index - k]] == 1)
                distinctCnt--;
            integers[A[index-k]]--;
            
            if(integers[A[index]] == 0)
                distinctCnt++;
            integers[A[index]]++;

            distinctIntegersPerWindow.push_back(distinctCnt);
        }
        return distinctIntegersPerWindow;
    }
};
```
