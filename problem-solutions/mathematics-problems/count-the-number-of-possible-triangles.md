# Count the number of possible triangles

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/count-possible-triangles-1587115620/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given an unsorted array **arr\[\]** of **n** positive integers. Find the number of triangles that can be formed with three different array elements as lengths of three sides of triangles. 

**Example 1:**

```text
Input: 
n = 3
arr[] = {3, 5, 4}
Output: 
1
Explanation: 
A triangle is possible 
with all the elements 5, 3 and 4.
```

**Example 2:**

```text
Input: 
n = 5
arr[] = {6, 4, 9, 7, 8}
Output: 
10
Explanation: 
There are 10 triangles
possible  with the given elements like
(6,4,9), (6,7,8),...
```

**Expected Time Complexity:** O\(n^2\).  
**Expected Space Complexity:** O\(1\).  
  
 **Constraints:**  
 3 &lt;= n &lt;= 10^3  
 1 &lt;= arr\[i\] &lt;= 10^3

### Algorithm

**For a triangle to be possible from 3 values, the sum of any of the two values \(or sides\) must be greater than the third value \(or third side\).**

First sort the array, and run a nested loop, fix an index and then try to fix an upper and lower index within which we can use all the lengths to form a triangle with that fixed index.

**Algorithm:**

1. Sort the array and then take three variables l, r and i, pointing to start, i-1 and i is array element starting from end of the array and decremented after each loop.
2. Traverse the array from end \(n-1 to 1\), and for each iteration keep the value of l = 0 and r = i-1
3. Now **if a triangle can be formed using arr\[l\] and arr\[r\] then triangles can obviously formed  from a\[l+1\], a\[l+2\].....a\[r-1\], arr\[r\] and a\[i\], because the array is sorted** , which can be directly calculated using \(r-l\). and then decrement the value of r and continue the loop till l is less than r
4. If a triangle cannot be formed using arr\[l\] and arr\[r\] then increment the value of l and continue the loop till l is less than r 
5. So the overall complexity of iterating through all array elements reduces.

```cpp
class Solution
{
public:
    int findNumberOfTriangles(int arr[], int n){
        int count = 0;
        sort(arr, arr+n);
        for(int largerSide = n-1; largerSide >= 1; largerSide--)
        {
            int smallerSide = 0, middleSide = largerSide - 1; 
            while(smallerSide < middleSide)
            {
                if(arr[smallerSide] + arr[middleSide] > arr[largerSide])
                {
                    count += middleSide - smallerSide;
                    middleSide--;
                }
                else
                {
                    smallerSide++;
                }
            }
        }
        return count;
    }
};
```

