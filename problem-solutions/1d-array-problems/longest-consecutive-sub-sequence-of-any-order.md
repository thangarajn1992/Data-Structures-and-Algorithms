# Longest consecutive sub-sequence of any order

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/longest-consecutive-subsequence2449/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Walmart](../../company-based-lists/walmart.md)

### Problem Statement

Given an array of positive integers. Find the length of the longest sub-sequence such that elements in the sub-sequence are consecutive integers, the **consecutive numbers can be in any order. **complete the function **findLongestConseqSubseq()** which takes the array arr\[] and the size of the array as inputs and returns the length of the longest sub-sequence of consecutive integers.\
  

**Example 1:**

```
Input:
N = 7
a[] = {2,6,1,9,4,5,3}
Output:
6
Explanation:
The consecutive numbers here
are 1, 2, 3, 4, 5, 6. These 6 
numbers form the longest consecutive
subsquence.
```

**Example 2:**

```
Input:
N = 7
a[] = {1,9,3,10,4,20,2}
Output:
4
Explanation:
1, 2, 3, 4 is the longest
consecutive subsequence.
```

**Expected Time Complexity:** O(N).\
**Expected Auxiliary Space:** O(N).\
**Constraints:**\
 1 <= N <= 10^5\
 0 <= a\[i] <= 10^5

### Solution

```cpp
class Solution{
public:
    int findLongestConseqSubseq(int arr[], int N)
    {
        set<int> mySet;
        for(int i = 0; i < N; i++)
            mySet.insert(arr[i]);
        
        set<int>::iterator it = mySet.begin();
        int maxConsecutive = 1;
        int curConsecutive = 1;
        int prev = *it;
        it++;
        for(; it!= mySet.end(); it++)
        {
            if(*it == prev + 1)
                curConsecutive++;
            else
            {
                if(curConsecutive > maxConsecutive)
                    maxConsecutive = curConsecutive;
                curConsecutive = 1; 
            }
            prev = *it;
        }
        if(curConsecutive > maxConsecutive)
            maxConsecutive = curConsecutive;
        return maxConsecutive;
        
    }
};
```
