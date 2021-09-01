# Majority Element

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/majority-element-1587115620/1#)
* [Leetcode 169](https://leetcode.com/problems/majority-element/)

### Companies

* [Google](../../company-based-lists/google.md)
* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given an array **A** of **N** elements. Find the majority element in the array. A majority element in an array A of size N is an **element that appears more than N/2 times in the array**.  
  

**Example 1:**

```text
Input:
N = 3 
A[] = {1,2,3} 
Output:
-1
Explanation:
Since, each element in 
{1,2,3} appears only once so there 
is no majority element.
```

**Example 2:**

```text
Input:
N = 5 
A[] = {3,1,3,3,2} 
Output:
3
Explanation:
Since, 3 is present more
than N/2 times, so it is 
the majority element.
  
```

**Expected Time Complexity:** O\(N\).  
**Expected Auxiliary Space:** O\(1\).  
  

**Constraints:**  
 1 ≤ N ≤ 10^7  
 0 ≤ A\[i\] ≤ 10^6

### Solution

#### Moore's Voting Algorithm

This is a two-step process. 

* The first step gives the element that maybe the majority element in the array. If there is a majority element in an array, then this step will definitely return majority element, otherwise, it will return candidate for majority element.
* Check if the element obtained from the above step is majority element. This step is necessary as there might be no majority element.

```cpp
int majorityElement(int a[], int size)
{
    int result = a[0], count = 0;
    for(int index = 0; index < size; index++)
    {
        if(count == 0)
            result = a[index];
        count += (result == a[index])? 1 : -1;
    }
    
    // when count <= 0, there is no majority element
    if(count <= 0) 
        return -1;
        
    // Now result has the probable majority element, check its frequency > size/2
    int frequency = 0;
    for(int index = 0; index < size; index++)
    {
        if(a[index] == result)
            frequency++;
    }
    return (frequency > size/2) ? result : - 1;
}
```

