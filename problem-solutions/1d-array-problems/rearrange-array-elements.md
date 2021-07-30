# Rearrange array elements

### Sources

* Elements of Programming Interviews





### Problem Statement

Write a program that takes an array A of n numbers, and rearranges A's elements to get a new array B having the property that B\[0\] &lt;= B\[1\] &gt;= B\[2\] &lt;= B\[3\] &gt;= B\[4\] &lt;= B\[5\] &gt;= ....

### Algorithm

One Straight forward solution is to sort A and interleave the bottom halves of the sorted arrays. O\(nlogn\)

Alternatively, we can sort A and then swap the elements at the pairs \( A\[1\], A\[2\]\), \(A\[3\], A\[4\],.. \). O\(nlogn\)

The Optimum solution is,

The desired ordering is very local, and realize that is not it is not necessary to sort the entire array or to find the median. We can just iterate through the array and swap A\[i\] and A\[i+1\] when i is even and A\[i\] &gt; A\[i+1\] or i is odd and A\[i\] &lt; A\[i+1\] to achieve the desired configuration.

### Solution

```cpp
void rearrange(vector<int>& arr)
{
    for(int i = 1; i < arr.size(); i++)
    {
        if( (!(i % 2) && A[i - 1] < A[i]) ||
              (i % 2) && A[i - 1] > A[i])
        {
            swap(A[i-1], A[i]);
        }
    }
}
```



