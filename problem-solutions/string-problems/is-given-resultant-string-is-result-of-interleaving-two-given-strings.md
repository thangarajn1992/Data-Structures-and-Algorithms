# Is given resultant string is result of interleaving two given strings

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/interleaved-strings/1#)

### Companies

* [Google](../../company-based-lists/google.md)
* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given strings **A**, **B**, and **C**, find whether **C** is formed by an interleaving of **A** and **B**.

An interleaving of two strings S and T is a configuration such that it creates a new string Y from the concatenation substrings of A and B and |Y| = |A + B| = |C|

For example:

A = "XYZ"

B = "ABC"

so we can make multiple interleaving string Y like, XYZABC, XAYBCZ, AXBYZC, XYAZBC and many more so here your task is to check whether you can create a string Y which can be equal to C.

Specifically, you just need to create substrings of string A and create substrings B and concatenate them and check whether it is equal to C or not.

Note: **a + b** is the concatenation of strings a and b.

Return **true** if **C** is formed by an interleaving of **A** and **B**, else return **false.**

**Example 1:**

```
Input:
A = YX, B = X, C = XXY
Output: 0
Explanation: XXY is not interleaving
of YX and X
```

**Example 2:**

```
Input:
A = XY, B = X, C = XXY
Output: 1
Explanation: XXY is interleaving of
XY and X.
```

**Your Task:**\
Complete the function **isInterleave() **which takes three strings A, B and C as input and returns true if C is an interleaving of A and B else returns false. (1 is printed by the driver code if the returned value is true, otherwise 0.)

**Expected Time Complexity:** O(N \* M)\
**Expected Auxiliary Space:** O(N \* M)\
here, N = length of A, and M = length of B

**Constraints:**\
1 ≤ length of A, B ≤ 100\
1 ≤ length of C ≤ 200

### Solution

```cpp
class Solution{
  public:
    /*You are required to complete this method */
    bool isInterleave(string A, string B, string C) 
    {
        if(C.size() != A.size() + B.size())
            return false;
        return isInterleaveValid(A, B, C, 0, 0, 0);
    }
    bool isInterleaveValid(string A, string B, string C, int AIndex, int BIndex, int CIndex)
    {
        if(CIndex == C.size())
            return true;
        
        if(AIndex < A.size() && A[AIndex] == C[CIndex])
            if(isInterleaveValid(A, B, C, AIndex+1, BIndex, CIndex+1))
                return true;
        
        if(BIndex < B.size() && B[BIndex] == C[CIndex])
            if(isInterleaveValid(A, B, C, AIndex, BIndex+1, CIndex+1))
                return true;
        
        return false;
    }                      
};
```
