# Missing number in array with elements 1 to n

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/missing-number-in-array1416/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Adobe](../../company-based-lists/adobe.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given an array of size **N-1** such that it only contains distinct integers in the range of **1 to N**. Find the missing element.Complete the function **MissingNumber()** that takes array and N as input  parameters and returns the value of the missing number.

**Example 1:**

```
Input:
N = 5
A[] = {1,2,3,5}
Output: 4
```

**Example 2:**

```
Input:
N = 10
A[] = {1,2,3,4,5,6,7,8,10}
Output: 9
```

**Expected Time Complexity:** O(N)\
**Expected Auxiliary Space:** O(1)\
&#x20;**Constraints:**\
&#x20;1 ≤ N ≤ 10^6\
&#x20;1 ≤ A\[i] ≤ 10^6

### Solution

#### Mathematics Formula for Sum of 'N' natural numbers

```cpp
class Solution{
  public:
    int MissingNumber(vector<int>& array, int n) {
        int total = (n * (n+1))/2;
        for(int &num : array)
            total -= num;
        return total;
    }
};
```

#### Xor Property

if `S1 ^ S2 ^ S3 ^ .... Sn = a` and  `S1 ^ S2 ^ S3 ^ ... ^ Sn-1 = b`, then `a ^ b = Sn`

```cpp
class Solution{
  public:
    int MissingNumber(vector<int>& array, int n) {
        int xortilln = 1;
        for(int i = 2; i <= n; i++)
            xortilln ^= i;
        
        int xorinarray = array[0];
        for(int i = 1; i < n-1; i++)
            xorinarray ^= array[i];
            
        return xortilln ^ xorinarray;
    }
};
```
