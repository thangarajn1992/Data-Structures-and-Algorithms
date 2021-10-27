# Rearrange array into 3 parts based on given pivot ( < , = , > pivot) Dutch Flag Partitioning

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/sort-an-array-of-0s-1s-and-2s4231/1#)
* [Leetcode 75](https://leetcode.com/problems/sort-colors/)
* EPI 6.1

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Samsung](../../company-based-lists/samsung.md)
* [Adobe](../../company-based-lists/adobe.md)
* [Walmart](../../company-based-lists/walmart.md)

### Problem Statement

Given an array of size N containing only 0s, 1s, and 2s; sort the array in ascending order. Complete the function **sort012()** that takes an array arr and N as input parameters and **sorts the array in-place.**

\
&#x20;**Example 1:**

```
Input: 
N = 5
arr[]= {0 2 1 2 0}
Output:
0 0 1 2 2
Explanation:
0s 1s and 2s are segregated 
into ascending order.
```

**Example 2:**

```
Input: 
N = 3
arr[] = {0 1 0}
Output:
0 0 1
Explanation:
0s 1s and 2s are segregated 
into ascending order.
```

**Expected Time Complexity:** O(N)\
**Expected Auxiliary Space:** O(1)

**Constraints:**\
&#x20;1 <= N <= 10^6\
&#x20;0 <= A\[i] <= 2

### Algorithm

We can reduce runtime, at the cost of a trickier implementation. We can perform classification into elements less than, equal to, and greater than the pivot in a single pass. We do this by maintaining four subarrays :&#x20;

1. **Bottom ( elements less than Pivot)**
2. **Middle ( elements equal to Pivot)**
3. **Unclassified**
4. **Top ( elements greater than Pivot)**

Initially all elements are in unclassified. We iteratre through elements in unclassified, and move elements into one of bottom, middle, and top groups according to the relative order between the incoming unclassified element and the pivot.

**Time Complexity : O(N)   Space Complexity : O(1)**

### Solution

```cpp
void sort012(int a[], int n)
{
    int smaller = 0, equal = 0, larger = n;
    int pivot = 1;
    while(equal < larger)
    {
        if(a[equal] < pivot){
            int temp = a[smaller];
            a[smaller] = a[equal];
            a[equal] = temp;
            smaller++, equal++;
        }
        else if(a[equal] == pivot)
            equal++;
        else
        {
            larger--;
            int temp = a[equal];
            a[equal] = a[larger];
            a[larger] = temp;
        }
    }
}
```
