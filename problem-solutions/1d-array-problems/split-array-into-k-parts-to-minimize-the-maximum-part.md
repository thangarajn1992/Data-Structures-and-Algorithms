# Split array into k parts to minimize the maximum part

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/allocate-minimum-number-of-pages0937/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Google](../../company-based-lists/google.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

You are given **N** number of books. Every ith book has **Ai** number of pages. \
 You have to allocate books to **M** number of students. There can be many ways or permutations to do so. In each permutation, one of the **M** students will be allocated the maximum number of pages. Out of all these permutations, the task is to find that particular permutation in which the maximum number of pages allocated to a student is minimum of those in all the other permutations and print this minimum value. 

Each book will be allocated to exactly one student. Each student has to be allocated at least one book.

**Note:** Return **-1** if a valid assignment is not possible, and **allotment should be in contiguous order (see the explanation for better understanding).**

\
 **Example 1:**

```
Input:
N = 4
A[] = {12,34,67,90}
M = 2
Output:
113
Explanation: 
Allocation can be done in following ways:
{12} and {34, 67, 90} Maximum Pages = 191
{12, 34} and {67, 90} Maximum Pages = 157
{12, 34, 67} and {90}  Maximum Pages =113
Therefore, the minimum of these cases is 
113, which is selected as the output.
```

**Example 2:**

```
Input:
N = 3
A[] = {15,17,20}
M = 2
Output:
32
Explanation:
Allocation is done as 
{15,17} and {20}
```

**Expected Time Complexity**: O(NlogN)\
**Expected Auxilliary Space**: O(1)

**Constraints:**\
 1 <= N <= 10^5\
 1 <= A \[ i ] <= 10^6\
 1 <= M <= 10^5

### Solution

#### Binary Search

```cpp
class Solution 
{
    public:
    int findPages(int arr[], int books, int students)
    {
        long long totalPages = 0;

        if (books < students)
            return -1;
 
        for (int bookNum = 0; bookNum < books; bookNum++)
            totalPages += arr[bookNum];
 
        // initialize start as 0 pages and end as
        // total pages
        int start = 0, end = totalPages;
        int result = INT_MAX;
 
        // traverse until start <= end
        while (start <= end)
        {
            // check if it is possible to distribute
            // books by using mid as current minimum
            int mid = start + (end - start)/ 2;
            if (isPossible(arr, books, students, mid))
            {
                result = mid;
                end = mid - 1;
            }
            else
                start = mid + 1;
        }
        return result;
    }
    
    // Utility function to check if current minimum value
    // is feasible or not.
    bool isPossible(int arr[], int books, int students, int minPageCount)  
    {
        int studentsRequired = 1;
        int currPageCount = 0;
 
        // iterate over all books
        for (int bookNum = 0; bookNum < books; bookNum++)
        {
            // check if current number of pages are greater
            // than curr_min that means we will get the result
            // after mid no. of pages
            if (arr[bookNum] > minPageCount)
                return false;
 
            // count how many students are required
            // to distribute minPageCount pages
            if (currPageCount + arr[bookNum] > minPageCount)
            {
                // increment student count
                studentsRequired++;
 
                // update curr_sum
                currPageCount = arr[bookNum];
 
                // If more students are needed, return false
                if (studentsRequired > students)
                    return false;
            }
            else
                currPageCount += arr[bookNum];
        }
        return true;
    }
};
```
