# Maximum of minimum for every window size

### Sources

* [GeeksForGeeks](https://practice.geeksforgeeks.org/problems/maximum-of-minimum-for-every-window-size3453/1)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Flipkart](../../company-based-lists/flipkart.md)

### Problem Statement

Given an integer array. The task is to find the maximum of the minimum of every window size in the array.\
**Note:** Window size varies from 1 to the size of the Array.

**Example 1:**

```
Input:
N = 7
arr[] = {10,20,30,50,10,70,30}
Output: 70 30 20 10 10 10 10 
Explanation: 
1.First element in output
indicates maximum of minimums of all
windows of size 1.
2.Minimums of windows of size 1 are {10},
 {20}, {30}, {50},{10}, {70} and {30}. 
 Maximum of these minimums is 70. 
3. Second element in output indicates
maximum of minimums of all windows of
size 2. 
4. Minimums of windows of size 2
are {10}, {20}, {30}, {10}, {10}, and
{30}.
5. Maximum of these minimums is 30 
Third element in output indicates
maximum of minimums of all windows of
size 3. 
6. Minimums of windows of size 3
are {10}, {20}, {10}, {10} and {10}.
7.Maximum of these minimums is 20. 
Similarly other elements of output are
computed.
```

**Example 2:**

```
Input:
N = 3
arr[] = {10,20,30}
Output: 30 20 10
Explanation: First element in output
indicates maximum of minimums of all
windows of size 1.Minimums of windows
of size 1 are {10} , {20} , {30}.
Maximum of these minimums are 30 and
similarly other outputs can be computed
```

**Your Task:**\
The task is to complete the function **maxOfMin**() which takes the array arr\[] and its size N as inputs and finds the maximum of minimum of every window size and returns an array containing the result.&#x20;

**Expected Time Complexity** : O(N)\
**Expected Auxiliary Space** : O(N)

**Constraints:**\
1 <= N <= 10^5\
1 <= arr\[i] <= 10^6

### Algorithm

We can solve this problem in O(n) time. The idea is to use extra space.&#x20;

Below are detailed steps.\
**Step 1:** Find indexes of next smaller and previous smaller for every element. Next smaller is the nearest smallest element on right side of arr\[i]. Similarly, a previous smaller element is the nearest smallest element on the left side of arr\[i].&#x20;

If there is no smaller element on the right side, then the next smaller is n.&#x20;

If there is no smaller on the left side, then the previous smaller is -1.

For input {10, 20, 30, 50, 10, 70, 30}, array of indexes of next smaller is {7, 4, 4, 4, 7, 6, 7}. \
For input {10, 20, 30, 50, 10, 70, 30}, array of indexes of previous smaller is {-1, 0, 1, 2, -1, 4, 4}.

**Step 2:** Once we have indexes of next and previous smaller, we know that arr\[i] is a minimum of a window of length “right\[i] – left\[i] – 1”. Lengths of windows for which the elements are minimum are {7, 3, 2, 1, 7, 1, 2}. This array indicates, the first element is minimum in the window of size 7, the second element is minimum in the window of size 3, and so on.

Create an auxiliary array ans\[n+1] to store the result. Values in ans\[] can be filled by iterating through right\[] and left\[]&#x20;

```
    for (int i=0; i < n; i++)
    {
        // length of the interval
        int len = right[i] - left[i] - 1;

        // arr[i] is a possible answer for
        // this length len interval
        ans[len] = max(ans[len], arr[i]);
    }
```

We get the ans\[] array as {0, 70, 30, 20, 0, 0, 0, 10}. Note that ans\[0] or answer for length 0 is useless.

\
**Step 3:** Some entries in ans\[] are 0 and yet to be filled. For example, we know maximum of minimum for lengths 1, 2, 3 and 7 are 70, 30, 20 and 10 respectively, but we don’t know the same for lengths 4, 5 and 6.

Below are few important observations to fill remaining entries \
a) Result for length i, i.e. ans\[i] would always be greater or same as result for length i+1, i.e., ans\[i+1]. \
b) If ans\[i] is not filled it means there is no direct element which is minimum of length i and therefore either the element of length ans\[i+1], or ans\[i+2], and so on is same as ans\[i] \
So we fill rest of the entries using below loop.&#x20;

```
    for (int i=n-1; i>=1; i--)
        ans[i] = max(ans[i], ans[i+1]);
```

### Solution

```cpp
class Solution
{
    public:
    //Function to find maximum of minimums of every window size.
    vector <int> maxOfMin(int arr[], int n)
    {
        // Used to find previous and next smaller
        stack<int> s;
 
        // Arrays to store previous and next smaller
        vector<int> left(n+1, -1); 
        vector<int> right(n+1, n);
 
        for (int i = 0; i < n; i++)
        {
            while (!s.empty() && arr[s.top()] >= arr[i])
                s.pop();
 
            if (!s.empty())
                left[i] = s.top();
 
            s.push(i);
        }
        
        // Empty the stack as stack is going to be used for right[]
        while (!s.empty())
            s.pop();
 
        // Fill elements of right[] using same logic
        for (int i = n-1 ; i >= 0 ; i--)
        {
            while (!s.empty() && arr[s.top()] >= arr[i])
                s.pop();
 
            if(!s.empty())
                right[i] = s.top();
 
            s.push(i);
        }
        
        vector<int> ans(n, 0);
        
        // Fill answer array by comparing minimums of all
        // lengths computed using left[] and right[]
        for (int i = 0; i < n; i++)
        {
            // length of the window
            int len = right[i] - left[i] - 1;
 
            // arr[i] is a possible answer for this length
            // 'len' interval, check if arr[i] is more than
            // max for 'len'
            // since there is no window of size 0, we start
            // window size from 1 but array index for ans starts from 0
            ans[len - 1] = max(ans[len - 1], arr[i]);
        }
  
        // Some entries in ans[] may not be filled yet. Fill
        // them by taking values from right side of ans[]
        for (int i = n-2; i >= 1; i--)
            ans[i] = max(ans[i], ans[i+1]);
        
        return ans;
    }
};w
```
